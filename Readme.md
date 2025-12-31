# TCGA-COAD Bayesian Causal Survival Analysis

This project studies the association between **first-course treatment response** and **progression-free interval (PFI)** in **TCGA colorectal adenocarcinoma (COAD)** using **propensity score matching** and **Bayesian survival models**.

---

## Study Design

- **Exposure**: First-course treatment response  
  (`treatment_outcome_first_course`, favorable vs unfavorable)
- **Outcome**: Progression-Free Interval (PFI)
- **Baseline confounders**: Age, gender, stage
- **Framework**: Causal inference via propensity score matching  

> Both exposure groups received treatment; the exposure represents **response status**, not treatment assignment.

---

## Analysis Workflow

1. Build COAD cohort from TCGA-CDR clinical data  
2. Estimate propensity scores  
   - PS = P(favorable response | baseline covariates)
   - Matching with balance diagnostics (SMD, Love plot)
3. Fit primary survival model  
   - Bayesian Weibull Accelerated Failure Time (AFT)
4. Conduct sensitivity analyses  
   - Cox proportional hazards model  
   - Bayesian AFT without age

---

## Key Results

- **Bayesian AFT**: Time ratio ≈ **6–7**
- **Cox PH**: HR ≈ **0.18**, directionally consistent
- Results robust across model specifications

---

## Takeaway

Among patients with comparable baseline characteristics, **favorable first-course treatment response is strongly associated with prolonged progression-free interval**.