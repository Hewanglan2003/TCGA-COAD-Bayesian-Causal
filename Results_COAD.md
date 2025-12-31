#### TCGA-COAD-Bayesian-Causal

### 00_setup
Download all the necessary packages for this project.

### 01_download
Download the TCGA-CDR-SupplementalTableS1 and screen the COAD data for this project.

### 02_build_cohort
We are to find the causal relationship between first time post-treatment effect and the PFI(Progression-free interval).
Expousre: treatment_outcome_first_course(expo_good)
Outcome : PFI time and PFI event
Confounders: Age, gender, stage
There are too many samples for expo_good = 1 so we need to balance them in next step.

### 03_ps_design
We use confounders as input and exposure as output to calculate the propensity score for each sample.
PS_i = P(Exposure = 1|baseline covariates) = P(favorable first-course response | baseline covariates).
Suppose two patients have the same PS score = 7.2 than we can based on age, gender, stage, both patients have a probaility of 72% showing positive response before any treatment was done.
We do PS matching to balance the sample size between two groups(expo_good = 1 and expo_good = 0).
Calualte the SMD to make sure the Matching really works. We find that the SMD of confounder age is still larger than 0.1 so we need to put that in the analysis in next step.
We also draw a love plot to show the different of pre-matching and post-matching.

### 04_bayes_survival
We apply Bayesian AFT Weibull Survival and the outcomes are PFI time and event. The variates are expo_good and age because we are focusing on the causal inference between expo_good and PFI.
Then we can get the time_ratio with a median 6.74.
We can think of it like the PFI time of patients with the positive response after treatment is 6.74 times longer than the patients with a negative response after first treatment.

### Sensitivity Analysis
If we change the model into the Cox Proportional hazard ratio model, can we get the same conclusion?

HR = 0.18
At any time, the patients with a favorable first-course response have about an 81% lower instant risk than the poor responders after first course.

Is there any overfitting of variable age in the model? We still use the Bayesian AFT Weibull model.
The time ratio has a median of 6.39 so we can suppose that there is no significant difference between two models. There is no overfitting for the variable age and we can beleive the robustness of the model.