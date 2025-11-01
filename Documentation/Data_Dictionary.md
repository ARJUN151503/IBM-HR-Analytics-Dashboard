# Data Dictionary - IBM HR Analytics Dataset

## Dataset Overview
- **Total Records**: 1,470 employees
- **Total Fields**: 35 attributes
- **Target Variable**: Attrition (Yes/No)
- **Missing Values**: None (100% complete data)

## Field Definitions

| Field Name | Data Type | Description | Values/Range | Example |
|-----------|-----------|-------------|--------------|---------|
| **EmployeeNumber** | Text | Unique employee identifier | 1-9999 | 1458 |
| **Age** | Number | Employee age in years | 18-60 | 35 |
| **Attrition** | Text | Whether employee left company | Yes, No | Yes |
| **BusinessTravel** | Text | Frequency of business travel | Travel_Rarely, Travel_Frequently, Non-Travel | Travel_Rarely |
| **Department** | Text | Employee's department | Sales, Research & Development, Human Resources | Sales |
| **DistanceFromHome** | Number | Distance from home to office (km) | 1-29 | 15 |
| **Education** | Number | Education level (ordinal) | 1=Below College, 2=College, 3=Bachelor, 4=Master, 5=Doctor | 3 |
| **EducationField** | Text | Field of education | Life Sciences, Medical, Marketing, Technical Degree, Other, Human Resources | Life Sciences |
| **EnvironmentSatisfaction** | Number | Workplace environment rating | 1=Low, 2=Medium, 3=High, 4=Very High | 3 |
| **Gender** | Text | Employee gender | Male, Female | Female |
| **JobInvolvement** | Number | Level of job involvement | 1=Low, 2=Medium, 3=High, 4=Very High | 3 |
| **JobLevel** | Number | Job hierarchy level | 1-5 (1=Entry, 5=Executive) | 2 |
| **JobRole** | Text | Specific job title | Sales Executive, Research Scientist, Laboratory Technician, Manufacturing Director, Healthcare Representative, Manager, Sales Representative, Research Director, Human Resources | Sales Executive |
| **JobSatisfaction** | Number | Job satisfaction rating | 1=Low, 2=Medium, 3=High, 4=Very High | 4 |
| **MaritalStatus** | Text | Marital status | Single, Married, Divorced | Married |
| **MonthlyIncome** | Number | Monthly salary (USD) | 1,009-19,999 | 6,503 |
| **NumCompaniesWorked** | Number | Number of previous companies | 0-9 | 2 |
| **OverTime** | Text | Whether employee works overtime | Yes, No | No |
| **PercentSalaryHike** | Number | Last salary increase percentage | 11-25% | 15 |
| **PerformanceRating** | Number | Latest performance review | 3=Excellent, 4=Outstanding | 3 |
| **RelationshipSatisfaction** | Number | Satisfaction with workplace relationships | 1=Low, 2=Medium, 3=High, 4=Very High | 3 |
| **StockOptionLevel** | Number | Stock option tier | 0-3 (0=None, 3=High) | 1 |
| **TotalWorkingYears** | Number | Total years of work experience | 0-40 | 10 |
| **TrainingTimesLastYear** | Number | Training sessions attended last year | 0-6 | 3 |
| **WorkLifeBalance** | Number | Work-life balance rating | 1=Bad, 2=Good, 3=Better, 4=Best | 3 |
| **YearsAtCompany** | Number | Years with current company | 0-40 | 5 |
| **YearsInCurrentRole** | Number | Years in current position | 0-18 | 2 |
| **YearsSinceLastPromotion** | Number | Years since last promotion | 0-15 | 1 |
| **YearsWithCurrManager** | Number | Years under current manager | 0-17 | 3 |

## Calculated Columns (Power Query)

| Column Name | Formula/Logic | Purpose |
|------------|---------------|---------|
| **Age Group** | IF Age < 25 THEN "Under 25" ELSE IF Age < 35 THEN "25-34" ... | Categorical age segmentation |
| **Income Range** | IF MonthlyIncome < 3000 THEN "Low" ELSE IF < 6000 THEN "Medium" ... | Income brackets |
| **Tenure Category** | IF YearsAtCompany < 2 THEN "0-2 years" ... | Tenure grouping |
| **Distance Category** | IF DistanceFromHome < 10 THEN "Near" ... | Commute distance grouping |

## DAX Measures

| Measure Name | Formula | Description |
|--------------|---------|-------------|
| **Total Employees** | COUNT('Employee Data'[EmployeeNumber]) | Total employee count |
| **Attrition Count** | CALCULATE(COUNT(...), Attrition = "Yes") | Number who left |
| **Attrition Rate %** | DIVIDE([Attrition Count], [Total Employees]) * 100 | Percentage turnover |
| **Active Employees** | CALCULATE(COUNT(...), Attrition = "No") | Current workforce |
| **Avg Monthly Income** | AVERAGE('Employee Data'[MonthlyIncome]) | Mean salary |

## Data Quality Notes

- ✅ No missing values
- ✅ No duplicate employee IDs
- ✅ All numeric fields within expected ranges
- ✅ Categorical fields have consistent values
- ⚠️ Removed columns: EmployeeCount (all 1), StandardHours (all 80), Over18 (all Yes) - no variance

## Target Variable Distribution

- **No (Stayed)**: 1,233 employees (83.9%)
- **Yes (Left)**: 237 employees (16.1%)
- **Slight class imbalance** - consider for predictive modeling
