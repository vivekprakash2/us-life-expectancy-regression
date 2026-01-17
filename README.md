# Predicting Life Expectancy Using Health, Social, and Environmental Indicators

## Overview
This project analyzes how **health behaviors, socioeconomic conditions, and environmental exposures** jointly influence **county-level life expectancy in the United States**. Using independently collected public datasets and **regression-based statistical modeling**, we identify the most influential predictors of life expectancy and evaluate how well these factors can explain and predict longevity outcomes.

The emphasis of this work is on **interpretability, statistical rigor, and validation of regression assumptions**, rather than purely black-box prediction.

---

## Objectives
The goals of this project are to:

1. Identify the **most important factors affecting life expectancy** across U.S. counties  
2. Build and compare **multiple regression models** using clear statistical metrics  
3. Evaluate **multicollinearity and regression assumptions**  
4. Balance **predictive performance and interpretability** through model reduction  

---

## Datasets Used
This analysis integrates three major public health datasets:

### 1. Environmental Justice Index (EJI)
- Census-tract–level indicators measuring environmental burden, social vulnerability, and health vulnerability  
- Aggregated to the **county level using population-weighted averages**  
- 36 indicators from CDC, EPA, Census Bureau, USGS, and DOT  

**Source:** CDC / ATSDR  

---

### 2. CDC PLACES: Local Data for Better Health
- County-level, model-based estimates of population health outcomes  
- Includes chronic disease prevalence, preventive care, and risk behaviors  
- Required reshaping from long format into a county-level feature matrix  

**Source:** CDC Division of Population Health  

---

### 3. County Health Rankings (CHR) – 2024
- County-level health outcomes and health-determinant measures  
- Includes education, income, healthcare access, behaviors, and environment  
- Minimal missingness (<2%), handled via mean imputation  

**Source:** University of Wisconsin Population Health Institute  

---

## Data Processing
Key preprocessing steps included:

- **Population-weighted aggregation** of census-tract EJI data to counties  
- **Pivoting PLACES data** into a standard X–Y matrix using Python  
- Cleaning and standardizing variable names  
- Converting character-encoded numeric variables  
- Merging datasets by **state + county** to avoid naming conflicts  

The final merged dataset contains **~3,000 counties and 91 variables**.

**Final Dataset**: [Google Drive Folder](https://drive.google.com/drive/u/0/folders/1Ef_fobxlxXsZmH_xIX9iGtMt1YsMgYg_) 

---

## Exploratory Data Analysis (EDA)
- Verified correct county alignment after merging  
- Inspected distributions and missingness  
- Standardized column naming for interpretability  
- Prepared dataset for regression modeling  

---

## Modeling Approach

### Simple Linear Regression
Used to assess **bivariate relationships** with life expectancy.

Key findings:
- Strong negative associations:  
  - Smoking  
  - Diabetes  
  - Obesity  
  - Food insecurity  
- Positive associations:  
  - Education  
  - Income  

These models provided intuition but did not account for confounding.

---

### Multiple Regression (Full Model)
- Included all numeric predictors (87 variables)  
- **R² ≈ 0.81**, indicating strong explanatory power  
- Many predictors remained significant after adjustment  

However:
- **Severe multicollinearity** (high VIFs) reduced interpretability  
- Motivated model reduction  

---

### Stepwise Regression (AIC-Based)
- Reduced to **56 predictors**  
- Maintained nearly identical performance  
- Significantly improved multicollinearity and interpretability  

---

### Further Reduced Model
- Final interpretable model with **37 predictors**  
- **Adjusted R² ≈ 0.79**  
- Minimal loss in explanatory power despite large reduction in variables  

This model was selected as the **preferred final model**.

---

## Interaction Effects
Several interaction terms were tested:

- **Smoking × Obesity** → statistically significant, small practical effect  
- **Food Insecurity × Education** → modest buffering effect  
- **Doctor Visits × % Female** → not significant  
- **% Black × Education** → statistically significant, negligible impact  

Overall, interactions provided **limited practical improvement** over main effects.

---

## Model Diagnostics
Standard regression diagnostics were performed:

- Residuals vs fitted: no strong nonlinearity  
- Q–Q plot: mild tail deviations (expected with large n)  
- Scale-location: minor heteroscedasticity  
- Leverage & Cook’s distance: no influential outliers  

**Conclusion:** Regression assumptions are reasonably satisfied for county-level analysis.

---

## Prediction
Using the reduced model:

- Predicted mean life expectancy: **72.26 years**  
- 95% confidence interval (mean): **[71.86, 72.65]**  
- 95% prediction interval (individual county): **[69.05, 75.47]**  

This highlights the difference between **population-level certainty** and **individual-level uncertainty**.

---

## Key Insights
- **Smoking and food insecurity** are among the strongest negative predictors  
- **Education** consistently shows strong positive association  
- Many variables are correlated, reinforcing the importance of model reduction  
- Life expectancy is driven by **interacting social, behavioral, and environmental systems**

---

## Limitations
- Correlated predictors limit causal interpretation  
- Some important factors (policy, local economics) not included  
- Cross-sectional analysis cannot establish causality  

---

## Technologies Used
- R (for diagnostics and modeling)  
- Excel (data cleaning)  
- Public health and census datasets  

---

## References
1. Khadke et al., *Journal of the American Heart Association*, 2024  
2. Chetty et al., *JAMA*, 2016  
3. Qiu et al., *Communications Medicine*, 2022  
