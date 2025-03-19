# Problem Description

I analyzed a dataset of hospital admissions to understand and predict respiratory disease patterns in Saudi Arabia, focusing on conditions like Asthma, COPD, and Other Respiratory Issues. The data included hourly records from 2022 to 2024 across multiple hospitals, with variables such as admission counts, patient demographics (age, gender), severity levels, environmental factors (temperature, humidity, PM2.5), and hospital locations. Initially, I aimed to find strong correlations between air pollutants (e.g., PM2.5) and respiratory admissions, expecting pollution to drive hospital visits. However, weak correlations (e.g., 0.005 for PM2.5 vs. admissions) shifted my focus to identifying broader patterns and building a predictive model. The goal became predicting monthly respiratory admissions per hospital with high accuracy to support healthcare planning, leveraging seasonal trends (e.g., May peak of 7,850 vs. November low of 4,741) and hospital-specific data (e.g., Riyadh’s 62% share).

## Step-by-Step Process

1. Explore Correlation
    - Started with a correlation analysis on the full dataset to link pollutants (PM2.5, NO2) and environmental factors (temperature, humidity) to health outcomes (admission_count, emergency_visit_count).
    - Result: Very weak correlations suggesting no strong linear pollution effect.
1. Filtered for Respiratory Subset
1. Shifted to Descriptive Analysis
    -Pivoted from correlations to trends due to persistent weak results.
        -Found:
            -Asthma led with 44,109 admissions, COPD 17,985, Other 17,603.
            -Riyadh hospitals (Riyadh National, King Saud, Riyadh General) handled 62%(49,356 admissions).
            -Monthly peak in May (7,850) vs. low in November (4,741).
1. Deepened Seasonal Insight
1. Built an ML Model
    - Goal: Predict monthly admissions per hospital with high accuracy.
    - Approach:
        - Aggregated by year, month, hospital for broader patterns.
        - Features: month, is_riyadh, hospital_name, temperature, humidity, value,  lag1_admissions (prior month’s count).
        - Model: Random Forest Regressor (n_estimators=100).
        - Result: MAE 46.85, R² 0.861—predictions off by ~47 admissions, explaining 86% of variance.

1. Evaluated Alternatives
    -Tuned Random Forest: MAE 44.89, R² 0.855 (max_depth=10).
    -XGBoost: MAE 46.90, R² 0.843.
    -Asthma-Only: MAE 24.70, R² 0.833.

### Final Outcome

I developed a predictive model that forecasts monthly respiratory hospital admissions with an MAE of 46.85 and R² of 0.861, meaning it’s accurate to within ~47 admissions and explains 86% of the variation. The model uses month, hospital location (Riyadh flag), and lagged admissions as key predictors, capturing the May peak (7,850) and November low (4,741) effectively. While PM2.5 didn’t drive admissions directly, the model’s high accuracy makes it valuable for hospital resource planning, especially in Riyadh, where 62% of cases occur.
