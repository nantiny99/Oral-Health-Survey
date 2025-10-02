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
   - Prevalence increases with age. Adults 75+ show the highest prevalence.  Both genders show the same amount of edentulism problem.

2. **Caries prevalence in children by race/ethnicity**  
   - Clear subgroup differences; some minority groups (Mexican) show higher caries prevalence than White non-Hispanic children.  

3. **Mean number of sealants per child since the 1990s**  
   - Average sealant counts increased across survey years, indicating preventive improvements.  

4. **Tooth types most affected among those with DMFT**  
   - Anteriors are the most affected teeth by DMFT followed by secondary molars.
   - 
5. **Does prevalence of caries increase by age?**  
   - Yes. Caries prevalence rises steadily with age.  

---

## EDA 2 — Fifteen Extended Analyses and Results

6. **Untreated caries by age**  
   - Increased age consistently shows a higher untreated caries prevalence.  

7. **Trends in filled teeth across survey periods**  
   - Mean filled teeth decreased gradually over time, reflecting greater treatment coverage.  

8. **Correlation of numeric variables**  
   - Estimate value and CI variables are strongly correlated; larger estimates usually come with larger SE and wider CIs.  

9. **Oral health indicators across years**  
   - Indicators show improvement across time (decayed teeth and missing teeth decreased); however, caries and edentulism are still prevalent across the years.
   - The ANOVA result tells us that there are meaningful differences in caries prevalence across time periods, and the Spearman correlation suggests that, overall, the          trend has been slightly downward

10. **Poverty status on caries and sealant**  
    - Strong socioeconomic status shows high sealants and prevalence of caries slightly higher in highly socioeconomic status
    - The ANOVA result shows that caries prevalence is not equal across education levels. People with different educational levels have significantly different caries rates.

11. **Sex differences**  
    - Both genders have almost the same level of prevalence of caries.
    - No statistically significant difference in caries prevalence between males and females.

12. **Caries by age**  
    - Caries prevalence increases with age, especially in adolescence and adulthood.
    - There is a strong relationship between age and caries.
 
13. **Socioeconomic disparities**  
    - The lowest SES groups and the Mexican racial group have a higher prevalence of caries compared with the highest SES groups and other racial groups.  

14. **Racial differences over time**  
    - Race and survey period both explain prevalence differences; subgroup trends vary across time.
    - Two-way ANOVA (years × race/ethnicity) for caries prevalence shows that neither years, race/ethnicity, nor their interaction was statistically significant
    - All p-values were much greater than 0.05. The R² was also very low (4.4%), meaning the model explains almost none of the variability.
    - This suggests that in this dataset, differences in caries prevalence are not strongly associated with time period or race/ethnicity.
    - The piecewise regression failed because there were not enough data points to fit such a model reliably

15. **Predictors of untreated caries**  
    - Poverty and education are the strongest predictors, followed by race and sex.
    - ROC AUC = 0.88 → The model is very good at distinguishing between people with caries and without caries (88% ranking ability).
    - Accuracy = 80% → Out of every 10 people, the model predicts correctly about 8 times.
    - Class 0 (no caries):
      - Precision = 0.76 → When the model says “no caries”, it’s right 76% of the time.
      - Recall = 0.85 → It correctly finds 85% of all the people without caries.
    - Class 1 (caries):
      - Precision = 0.84 → When the model says “caries”, it’s correct 84% of the time.
      - Recall = 0.75 → It catches 75% of actual caries cases (but misses about 25%).

16. **Model for edentulism by age**  
    - The exponential model explains the data better than the linear model
    - Since exponential fits better than linear, edentulism doesn’t change in a straight line over time.
      
17. **Estimate precision and uncertainty**  
    - Large subgroups provide stable estimates; small subgroups show high variability.
    - Age (65-74) has more influence and is more precise, as the inverse weighted mean is higher than the rest.
    - Age (20–34) has the smallest coefficient of variation as its estimate is the most precise relative to its mean.
    - Edentulism is much higher among people with low education and lower income, while younger adults have a very low prevalence.
    - The age estimate is highly precise, so it strongly informs pooled results, but education and poverty show clear disparities in tooth loss.

18. **Subgroup profiles across indicators**  
    - Gini and Theil measure inequality across groups.
    - Edentulism shows the highest inequality, followed by untreated caries, meaning these problems are concentrated in certain groups.
    - Caries overall has moderate inequality, while sealants are distributed most evenly.

---

## Requirements

* Python 3.x
* pandas, numpy
* matplotlib, seaborn
* statsmodels
* scikit-learn
