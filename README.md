# COVID-19 Risk

## Introduction

This report outlines the comprehensive steps taken in the data exploration and mining process for Nexoid’s medical dataset, focusing on COVID-19 risk factors and infection statuses. The objective was to analyze, clean, and prepare the dataset to ensure reliable insights in subsequent analysis phases.

Each section in this report addresses one of the following tasks:

1. **Examine and Correct Data Types**: Identify initial data types and correct mismatches for consistency.
2. **Prepare Data**: Address skewness, missing values, and other quality issues using cleaning and transformation methods.
3. **Data Mining Task and Feature Selection**: Explore relationships between variables, perform feature selection, and determine suitable data mining tasks.

## Task 1: Examine and Correct Data Types

### Step 1: Data Type Review and Initial Assessment

Initial analysis of data types was conducted using `df.dtypes`. Key issues identified included incorrect formats for date fields and categorical variables, which could impede analysis.

### Step 2: Convert Data Types

- **Convert Dates to DateTime**: The `survey_date` column was converted from string to `datetime64[ns]` to enable time-based operations.
- **Categorical Data**: Columns like `gender`, `region`, and `smoking` were converted to categorical data types to improve performance and ensure consistency.
- **Counts to Integers**: Variables like `contacts_count` were converted to integers to reflect their nature as whole numbers.
- **Boolean Data**: Binary fields such as `covid19_positive` and `heart_disease` were set to Boolean types for clarity and storage efficiency.
- **Age Data**: Age ranges were standardized to numerical midpoints (e.g., "20-25" became 22.5) to enhance granularity in analysis.
- **Height and Weight**: These columns were converted to `float64` for precision.

### Step 3: Review and Confirm Updates

Data types were reviewed after conversion to ensure alignment with intended formats, resolving any issues related to mixed data types.

---

## Task 2: Prepare Data

### Step 1: Check for Skewness

Skewness in the dataset was measured using `.skew()`, revealing extreme positive and negative skewness in variables like `public_transport_count` and `risk_mortality`. Addressing these distributions was critical to ensure robust analysis.

### Step 2: Plot Skewed Columns

Highly skewed columns were visualized to identify potential anomalies. Extreme skewness in variables like `cocaine` and `public_transport_count` was noted for further transformation.

### Step 3: Handle Missing Values

A detailed examination of missing values across columns revealed significant gaps in some variables. The following approaches were used:

- **Drop Columns with >50% Missing Data**: Columns like `cocaine` were removed to avoid introducing bias.
- **Impute Categorical Data**: Missing categorical values were replaced with "Unknown" to maintain dataset integrity.
- **Numerical Data Imputation**: Median values were used to replace missing numerical entries, ensuring robustness in non-normally distributed data.

### Step 4: Address Data Inconsistencies

Inconsistencies were addressed by:

- Standardizing categorical entries (e.g., consolidating smoking responses).
- Ensuring uniform formats for columns like `gender` and `blood_type`.
- Resolving issues where "NA" in the `region` column was misinterpreted as missing data.

### Step 5: Skewness Transformation

A cube root transformation was applied to reduce skewness, stabilizing variance and minimizing the impact of extreme values. This transformation effectively normalized highly skewed variables like `BMI` and `risk_mortality`.

Key outcomes:
- Skewness in `BMI` was reduced from 1.99 to 1.05.
- Skewness in `alcohol` dropped from 1.84 to 0.16.
- While some columns retained moderate skewness, the transformations significantly improved data symmetry.

---

## Task 3: Select Data Mining Task and Feature Selection

### Analysis of the Relationship Between COVID-19 Positivity and Smoking

A Chi-Square test was conducted to assess the association between smoking status and COVID-19 positivity. The results revealed a significant relationship, with a high Chi-Square value and a low p-value (< 0.001).

### Correlation Analysis

A correlation matrix highlighted key relationships:
- **Positive Correlations**: Strong relationships were observed between variables like `BMI` and `weight`.
- **Negative Correlations**: Notable negative correlations included `cluster` and `bmi_risk_infection_interaction`.

### Data Mining Task Selection

Given the dataset's structure and objectives:
- **Classification**: Selected to predict COVID-19 positivity based on health, demographic, and behavioral data.
- **Clustering**: Explored as an alternative for grouping individuals based on feature similarity.

### Feature Selection

The following features were selected for their relevance to predicting COVID-19 status:
- Health: `BMI`, `risk_infection`, `risk_mortality`.
- Behavioral: `contacts_count`, `public_transport_count`.
- Demographic: `age_mean`.
- Derived: `bmi_risk_infection_interaction`.

---

## Conclusion

This report details the comprehensive data preparation process undertaken to enhance the Nexoid dataset. Key outcomes include improved data quality, normalized distributions, and insights into variable relationships. These efforts provide a solid foundation for advanced analysis and reliable predictions in subsequent phases.
