# Survival After Pediatric Hematopoietic Stem Cell Transplantation

### Does the Stem-Cell Source Matter, or Is It the CD34+ Cell Dose?

A data science and survival analysis project investigating the relationship between stem-cell source, CD34+ cell dose and post-transplant survival in pediatric hematopoietic stem cell transplantation (HSCT).

---

## Overview

Hematopoietic stem cell transplantation (HSCT) is a potentially curative treatment for children with various hematological and immune-related disorders. However, post-transplant outcomes vary, making the identification of factors associated with survival and recovery an important area of clinical research.

This project investigates whether the source of transplanted stem cells — peripheral blood (PB) or bone marrow (BM) — is associated with overall survival in pediatric patients, and whether this association remains after accounting for CD34+ cell dose and other clinical characteristics.

Using statistical survival analysis and machine learning, the project examines transplant outcomes, evaluates predictive performance and explores the relationship between graft characteristics and patient recovery.

## Research Questions & Hypotheses

The analysis focuses on three main hypotheses:

- **H1a — Stem-cell source:** Is stem-cell source associated with overall survival?
- **H1b — Source and CD34+ dose:** Does the association between stem-cell source and survival weaken after accounting for CD34+ cell dose?
- **H2 — CD34+ dose:** Is a higher CD34+ cell dose associated with longer overall survival after adjustment for clinical factors?

A secondary analysis investigates whether stem-cell source and CD34+ dose influence neutrophil and platelet engraftment.

## Dataset

**Source:** [UCI Machine Learning Repository — Bone Marrow Transplant: Children](https://archive.ics.uci.edu/dataset/565/bone+marrow+transplant+children)

The dataset contains information on 187 pediatric patients undergoing unrelated-donor hematopoietic stem cell transplantation.

| Characteristic | Value |
|---|---:|
| Pediatric patients | 187 |
| Variables | 37 |
| Deaths during follow-up | 85 (45%) |
| Alive at last follow-up | 102 |
| Peripheral blood transplants | 145 |
| Bone marrow transplants | 42 |
| Median follow-up | 676 days |

The dataset includes demographic, clinical and transplant-related characteristics, alongside survival and post-transplant outcome information.

## Methodology

The project follows four analytical stages.

### 1. Descriptive Analysis & Survival Exploration

- Exploratory Data Analysis (EDA).
- Patient and transplant characteristic analysis.
- CD34+ dose distribution by stem-cell source.
- Kaplan–Meier survival estimation.
- Log-rank comparison of peripheral blood and bone marrow survival curves.

### 2. Statistical Modelling & Survival Analysis

Cox proportional hazards regression was used to investigate the association between stem-cell source and overall survival.

A sequence of models was developed:

- **Model 1:** Stem-cell source.
- **Model 2:** Stem-cell source and CD34+ cell dose.
- **Model 3:** Additional adjustment for age, risk group and disease.
- **Model 3q:** Extension incorporating a quadratic age term to investigate a potential non-linear age effect.

Additional analyses included:

- Wald tests and likelihood ratio tests.
- Proportional hazards assumption assessment using Schoenfeld residuals.
- Bootstrap analysis with 1,000 resamples to assess attenuation of the source effect.
- Sensitivity analyses to examine the robustness of the findings.

### 3. Machine Learning & Predictive Evaluation

A Random Survival Forest (RSF) model was compared against Cox regression approaches.

Model evaluation included:

- 5 × 5-fold cross-validation.
- Harrell's C-index.
- Integrated Brier score.
- Comparison of training and held-out performance.
- Permutation-based feature importance.

The objective was to assess whether more flexible machine learning approaches improved survival prediction compared with simpler statistical models.

### 4. Secondary Analysis: Engraftment Outcomes

Neutrophil and platelet recovery were investigated using competing-risk methods.

The analysis incorporated:

- Aalen–Johansen cumulative incidence estimation.
- Cause-specific Cox regression.
- Death before engraftment as a competing event.
- Assessment of stem-cell source and CD34+ dose in relation to recovery times.

## Key Findings

### 1. Stem-cell source and overall survival

Peripheral blood recipients initially showed better estimated survival than bone marrow recipients. However, the unadjusted log-rank result was borderline (p = 0.050), and the association was not statistically significant after adjustment.

### 2. CD34+ cell dose and stem-cell source

Peripheral blood grafts delivered approximately 3.3 times the median CD34+ cell dose of bone marrow grafts.

Adding CD34+ dose to the Cox model attenuated the estimated source effect by approximately 46%. However, the bootstrap confidence interval included zero, meaning this attenuation was not statistically confirmed.

### 3. CD34+ dose and survival

Higher CD34+ cell dose was not significantly associated with longer overall survival after adjustment for clinical factors.

### 4. Age and clinical characteristics

Age demonstrated a non-linear, U-shaped association with survival, with the lowest estimated risk around 7–8 years.

Lymphoma was also associated with higher mortality compared with acute lymphoblastic leukaemia (ALL) in the final Cox model.

### 5. Predictive performance

The simpler Cox model achieved a held-out C-index of approximately 0.59, compared with 0.57 for the Random Survival Forest.

The results suggest that more complex modelling did not improve generalisation in this relatively small cohort.

### 6. Engraftment outcomes

Peripheral blood grafts were associated with faster neutrophil and platelet recovery.

After adjustment, CD34+ dose remained associated with faster recovery, whereas stem-cell source was no longer statistically significant.

## Main Conclusion

The findings highlight the importance of distinguishing between factors associated with transplant recovery and those associated with long-term survival.

Although peripheral blood grafts were associated with faster engraftment and initially appeared to have better survival outcomes, the adjusted survival analysis did not establish a statistically significant independent effect of stem-cell source or CD34+ cell dose.

Age and disease characteristics provided more relevant information for survival modelling, although overall predictive performance remained modest.

Importantly, the absence of statistical significance should not be interpreted as proof that no clinical effect exists.

## Limitations & Future Research

Several limitations should be considered:

- Relatively small cohort (187 patients and 85 deaths).
- Unequal distribution between peripheral blood and bone marrow recipients.
- Observational design and potential confounding.
- Small clinical subgroups, particularly lymphoma.
- Internal validation only, without an independent external cohort.
- Limited statistical power to detect moderate associations.

Potential future directions include replication in larger transplant registries, formal mediation analysis, time-dependent modelling of GvHD and relapse, and external validation of predictive models.

## Repository Contents

| File | Description |
|---|---|
| [Presentation (PDF)](./Survival%20After%20Pediatric%20HSCT%20Presentation.pdf) | Full research presentation, methodology and findings |
| [Jupyter Notebook](./DSHC_V3.ipynb) | Data preparation, statistical analysis, survival modelling and machine learning |
| [Dataset](./bone-marrow.arff) | Original Bone Marrow Transplant: Children dataset |

## Technologies & Analytical Methods

- Python
- Jupyter Notebook
- Exploratory Data Analysis
- Statistical Inference
- Survival Analysis
- Kaplan–Meier Estimation
- Cox Proportional Hazards Regression
- Random Survival Forest
- Competing-Risk Analysis
- Cross-Validation
- Model Evaluation & Interpretation

## Team

Group 1 — MSc Applied Data Science and AI, Lucerne University of Applied Sciences and Arts (HSLU).

- Ibtihel Frini
- Yasna Ahmad
- Paula Barghout

## References

Sikora, M. & Wróbel, Ł. *Bone Marrow Transplant: Children*. UCI Machine Learning Repository.

Kaplan, E. L. & Meier, P. (1958). Nonparametric estimation from incomplete observations. *Journal of the American Statistical Association*, 53(282).

Cox, D. R. (1972). Regression models and life-tables. *Journal of the Royal Statistical Society: Series B*, 34(2).

Ishwaran, H. et al. (2008). Random survival forests. *The Annals of Applied Statistics*, 2(3).

Aalen, O. O. & Johansen, S. (1978). An empirical transition matrix for non-homogeneous Markov chains. *Scandinavian Journal of Statistics*, 5(3).

## Disclaimer

This project was developed for academic and research purposes. The results are exploratory and should not be interpreted as clinical recommendations or used for individual patient-level decision-making.
