# Financial-Inclusion-of-India
District-level econometric analysis of the **"Inclusion Gap"** between the 2011 Census baseline and CKYCR (Central KYC Registry) registrations till 31 December 2025, used as a proxy for digital financial identity.

# District-Level Financial Inclusion in India: Census 2011 vs CKYCR 2025

District-level econometric analysis of the **"Inclusion Gap"** between the 2011 Census
baseline and CKYCR (Central KYC Registry) registrations till 31 December 2025, used as a
proxy for digital financial identity. Built in **R**.

## Objective
- Quantify the gap between CKYCR registrations and the 2011 Census population at district level
- Measure how **bank branch density** and **literacy** drive CKYCR saturation
- Test structural penalties: urban hubs, tribal belt, backward districts, crime/LWE-affected areas
- Identify **"Hidden Champions"** (over-performers) and **under-performing districts** using residual analysis
- Visualise districts that lag behind peers with similar resources using heatmaps

## Data Source
| Census of India 2011 | Population and literacy baseline |
| CKYCR (CERSAI) till 31 Dec 2025 | Financial inclusion proxy |
| RBI Banking Outlet data (till 28 Jan 2026) | Branch density per lakh population |
| NITI Aayog Aspirational Districts Programme | Backward district classification |

**Data wrangling:**
- Districts created after 2011 were mapped back to their 2011 **parent districts**
- Population and literacy were adjusted to **permanent residents** (migrants with under 5 years of residence excluded)
- Study restricted to 22 key states for consistency (states that were split after 2011, and saturated states like Kerala, Tamil Nadu, Delhi, Karnataka, were left out)

> The dataset is not included in this repository.

## Methodology
1. **OLS regression**: CKYC coverage vs literacy, branch density and dummies
2. **Robust regression (RLM, MASS)**: down-weights influential districts
3. **lmrob (KS2014 setting)**: high-breakdown robust estimator, preferred model
4. **Dummy variables**: Urban, Tribal/Backward, Crime (as applicable per state)
5. **Influence diagnostics**: Cook's distance, leverage (hat values), leave-one-out sensitivity
6. **Frisch-Waugh-Lovell**: isolates independent effect of literacy and branches
7. **Performance adjustment**: Adjusted KYC and Counterfactual KYC to remove the "urban advantage"
8. **Classification and heatmaps**: Actual vs Predicted vs Deviation by district

## Key Findings
- **Urban premium is the strongest driver.** Urban hubs have about **18.4 percentage points** higher CKYC coverage in Gujarat and about **26.9 points** in Uttar Pradesh.
- **Literacy matters more than branches.** In Gujarat, a 1% rise in literacy corresponds to about 0.67% higher coverage, versus about 0.16% for branch density. In UP, the literacy coefficient is about 0.54, compared with about 0.04 for branches.
- **The gap is now a literacy gap, not a bank-access gap.** In lagging regions, adding branches alone gives limited gains.
- **Structural penalties exist.** In Madhya Pradesh, crime/LWE-affected districts (Chambal belt, Balaghat) show about 16% lower coverage even after controlling for literacy and urbanisation.
- **Hidden Champions after urban adjustment:** Anand and Kheda (Gujarat), Varanasi, Mathura and Aligarh (UP), Ujjain and Mandsaur (MP).
- **Persistent laggards:** tribal belt districts in Gujarat, backward and crime-belt districts in MP and UP.

## Policy Recommendations (summary)
- Document-literacy camps in tribal/backward areas rather than only opening branches
- Local Business Correspondents and digital onboarding in conflict-affected zones
- Replicate the cooperative-led models of Anand/Kheda in lagging regions
- Keep leveraging PMJDY and DBT for onboarding
