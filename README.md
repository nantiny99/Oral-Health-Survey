# Oral Health Survey - Data Cleaning & EDA Summary

## Project Overview
This repository contains exploratory data analysis of national oral health surveillance data.  
The primary dataset used is a cleaned demo table containing subgroup-level estimates (prevalence/means) and associated uncertainty (SE, lower_CI, upper_CI).  

The goal of the analysis is to describe trends, group differences, and data reliability for key oral-health indicators such as:
- Caries  
- Untreated caries  
- Sealants  
- Filled teeth  
- Edentulism  

---

## Data Cleaning — Actions Performed
- Renamed the unnamed identifier column to `data_id`.  
- Inspected missing values and calculated missing-value percentages for each column.  
- Replaced missing values in `tooth_location` with the most frequent category (mode).  
- Replaced missing numeric values (`estimate_value`, `estimate_SE`, `lower_CI`, `upper_CI`) with the median.  
- Visualized numeric distributions with histograms and boxplots to check skewness and outliers.  
- Did not delete outliers; instead used robust (median) imputation.  
- Fixed formatting issues in categorical labels:  
  - Corrected Excel-parsed age ranges (e.g., `"9-Nov"` → `"9–11"`).  
  - Normalized dash styles and cleaned inconsistent labels.  
- Saved cleaned dataset as `demo_clean.csv`.  

---

## EDA 1 — Five Primary Questions and Results

1. **Edentulism among adults 65+**  
   - Prevalence increases with age. Adults 75+ show the highest prevalence.  

2. **Caries prevalence in children by race/ethnicity**  
   - Clear subgroup differences; some minority groups show higher caries prevalence than White non-Hispanic children.  

3. **Mean number of sealants per child since the 1990s**  
   - Average sealant counts increased across survey years, indicating preventive improvements.  

4. **Tooth types most affected among those with DMFT**  
   - Molars, especially first molars, consistently show the highest burden.  

5. **Does prevalence of caries increase by age?**  
   - Yes. Caries prevalence rises steadily with age.  

---

## EDA 2 — Fifteen Extended Analyses and Results

6. **Untreated caries by poverty status**  
   - Lower-income groups consistently show higher untreated prevalence.  

7. **Trends in filled teeth across survey periods**  
   - Mean filled teeth increased over time, reflecting greater treatment coverage.  

8. **Correlation of numeric variables**  
   - Estimate and CI variables are strongly correlated; larger estimates usually come with larger SE and wider CIs.  

9. **Oral health indicators across years**  
   - Indicators show improvement across time (e.g., fewer untreated caries, more filled teeth).  

10. **Poverty status and education effects**  
    - Strong socioeconomic gradients: lower education and income groups show worse outcomes.  

11. **Sex differences**  
    - Males tend to have higher untreated prevalence; females show higher treated measures. Gaps narrowed in recent years.  

12. **Caries by age**  
    - Caries prevalence increases with age, especially in adolescence and adulthood.  

13. **Edentulism reliability checks**  
    - Smaller subgroups often have wide CIs and a high coefficient of variation (CV), reducing reliability.  

14. **Correlation across indicators**  
    - Caries, untreated caries, and DMFT are strongly correlated, indicating co-occurrence of burden.  

15. **Socioeconomic disparities**  
    - The lowest SES groups often have multiple times higher prevalence compared with the highest SES groups.  

16. **Racial differences over time**  
    - Race and survey period both explain prevalence differences; subgroup trends vary across time.  

17. **Predictors of untreated caries**  
    - Poverty and education are the strongest predictors, followed by race and sex.  

18. **Model for edentulism by age**  
    - A linear rise with age fits best; prevalence increases steadily with each age group.  

19. **Estimate precision and uncertainty**  
    - Large subgroups provide stable estimates; small subgroups show high variability.  

20. **Subgroup profiles across indicators**  
    - Groups with high caries also tend to have high untreated rates and lower preventive measures.  

---

## Requirements

* Python 3.x
* pandas, numpy
* matplotlib, seaborn
* statsmodels
* scikit-learn
