 **SAS Analysis of Drug Treatment Impact on Fasting Blood Sugar**
 
**Project Overview**

This project analyzes a synthetic clinical dataset using SAS to evaluate whether Drug A reduces fasting blood sugar levels in patients. The study includes 3,400 patients randomly assigned to three treatment groups: Low Dose Drug A, High Dose Drug A, and Placebo.

The analysis demonstrates practical applications of SAS for healthcare data management, statistical testing, and exploratory analysis, including dataset merging, sampling, distribution analysis, and hypothesis testing.
Study Design

A simulated clinical study was **conducted to examine the effectiveness of Drug A in lowering fasting blood sugar levels**.

Sample size: 3,400 patients

Study duration: 10 weeks

**Treatment Groups:** 

1. Low Dose Drug A

2. High Dose Drug A

3. Placebo

Patients were distributed across three clinical sites and belonged to multiple U.S. states.

**Dataset Description**

The dataset includes the following variables:

Variable	Description: 
Patient_ID - Unique identifier for each patient
Age -	Age of the patient
State - State of residence
Site -	Clinical study site (1–3)
Length_of_Stay -	Duration of stay during study period
Total_Charges -	Healthcare cost incurred
Fasting_BS -Fasting blood sugar level
Treatment_Group -	High dose, Low dose, or Placebo

Note: This dataset is synthetic.

**Data Preparation**
Importing Data : Two CSV datasets were imported into SAS after converting them into tab-delimited format.

**Data Cleaning**

Key preprocessing steps included:

1. Renaming the variable Test_Scores → Fasting_BS

2. Removing missing values

3. Standardizing variable formats

**Data Merging**

The datasets were merged using Patient_ID as the unique identifier.

```sas
data merged_dataset;
    merge dataset1 dataset2;
    by Patient_ID;
run;
```

**Steps performed:**

Sorting both datasets using **PROC SORT**

```sas
proc sort data=dataset1;
    by Patient_ID;
run;

proc sort data=dataset2;
    by Patient_ID;
run;
```

Performing a horizontal merge using the common key variable.

**Sampling Method**

A Simple Random Sampling (SRS) technique was used to generate a representative sample from the dataset for statistical analysis.

**Exploratory Data Analysis**

Several SAS procedures were used to understand the data:

1. Distribution analysis of variables

2. Frequency distribution of Total Charges

3. Patient enrollment distribution across states and treatment groups

**Key SAS procedures used:**

a. PROC SORT

b. PROC FREQ

c. PROC UNIVARIATE

d. PROC MEANS

**Research Questions**
**1. Does Drug A reduce fasting blood sugar levels?**

**Hypothesis**

Null Hypothesis (H₀)
There is no difference in fasting blood sugar levels between the three groups.

Alternative Hypothesis (H₁)
There is a difference in fasting blood sugar levels between the treatment groups.

**Statistical Test Used**

**One-Way ANOVA**
This test was selected because:

One independent variable: Treatment Group

Three categories: High, Low, Placebo

Assumption:

Data follows a normal distribution

Normality was checked using **PROC UNIVARIATE**.
```sas
proc univariate data=merged_dataset normal;
    var Fasting_BS;
run;
```

```sas
proc anova data=merged_dataset;
    class Treatment_Group;
    model Fasting_BS = Treatment_Group;
    means Treatment_Group / scheffe;
run;
```

**2. Is there a relationship between Age and Fasting Blood Sugar?**

Hypothesis

Null Hypothesis (H₀)
There is no correlation between age and fasting blood sugar levels.

Alternative Hypothesis (H₁)
There is a correlation between age and fasting blood sugar levels.

Correlation analysis was conducted to evaluate this relationship using **PROC CORR**

```sas
proc corr data=merged_dataset;
    var Age Fasting_BS;
run;
```

**Key Results**

**ANOVA Results**

The analysis indicates a significant difference in mean fasting blood sugar levels between treatment groups.

**Post-hoc comparison using Scheffé’s test** showed a statistically significant difference between:

Low Dose Drug A

Placebo

This suggests that Drug A has an effect on fasting blood sugar levels.

**Correlation Analysis**

A weak positive correlation was observed between:

Age

Fasting blood sugar levels

The result was statistically significant (p < 0.0001), indicating that fasting blood sugar tends to increase slightly with age.

