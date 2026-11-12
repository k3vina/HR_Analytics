# HR Analytics Dashboard: Employee Attrition Analysis (Excel)

An end-to-end Excel project that takes three raw HR datasets, cleans and merges them with Power Query, analyses the workforce with formulas and PivotTables, and presents the results in an interactive dashboard with data-driven recommendations.

**Author:** Kevina
**Tools:** Microsoft Excel (Power Query, PivotTables, PivotCharts, Slicers, Excel formulas)
**Course:** Zindua School, Data Analytics

---

## Project goal

Take **raw, fragmented data → clean it → analyse it → communicate meaningful insights → recommend actions**, with a focus on understanding why employees leave the organisation.

## Data sources

| File | Description | Rows | Columns |
|---|---|---|---|
| `general_data.csv` | Employee information (demographics, role, pay, tenure, attrition) | 4,410 | 24 |
| `employee_survey_data.csv` | Employee ratings: environment satisfaction, job satisfaction, work-life balance | 4,410 | 4 |
| `manager_survey_data.csv` | Manager ratings: job involvement, performance rating | 4,410 | 3 |

All three files share the key **EmployeeID**.

## Workflow

### 1. Import and explore (Power Query)
- Imported all three CSVs with Power Query and profiled every column (column quality, distribution, profile on the full dataset).
- Checked record counts, data types, missing values, duplicates, inconsistent values and unnecessary columns.

### 2. Clean and transform (Power Query)
| Issue | Fix |
|---|---|
| "NA" text in NumCompaniesWorked (19) and TotalWorkingYears (9) | Replaced with null, converted to whole number |
| "NA" text in EnvironmentSatisfaction (25), JobSatisfaction (20), WorkLifeBalance (38) | Replaced with null, converted to whole number |
| EmployeeCount, Over18, StandardHours hold one value for every row | Removed |
| BusinessTravel values use underscores (`Travel_Rarely`) | Standardised to "Travel Rarely" / "Travel Frequently" |
| Duplicate check on EmployeeID | No duplicates found; ID confirmed suitable for merging |

### 3. Merge
- Merged **Employee Information + Employee Survey + Manager Survey** on EmployeeID using Left Outer joins.
- Verified both merges matched **4,410 of 4,410 rows**. Final dataset: **4,410 rows × 26 columns**, loaded as the `HR_Clean` table.

### 4. Calculated fields (Excel formulas)
| Field | Logic |
|---|---|
| AgeBand | 18-25, 26-35, 36-45, 46-55, 56-60 |
| IncomeBand | Under 25K, 25K-50K, 50K-100K, 100K-150K, 150K+ |
| TenureBand | Years at company: 0-2, 3-5, 6-10, 11-20, 20+ |
| ExperienceBand | Total working years in the same bands (blank = Unknown) |
| SatisfactionScore | Average of the three employee survey ratings |
| SatisfactionCategory | Low (<2), Medium (2–<3), High (3+), Not Answered |
| AttritionFlag | 1 if Attrition = "Yes", else 0 (average = attrition rate) |

### 5. HR analysis (PivotTables)
- **Workforce:** headcount, average income and experience by department; average income by job role.
- **Satisfaction:** job satisfaction, work-life balance and environment satisfaction by department.
- **Attrition:** rate by department, job role, age band, tenure, business travel and experience band.

### 6. Interactive dashboard
- **KPI cards:** Total Employees, Attrition Rate, Average Monthly Income, Average Job Satisfaction, Average Performance Rating.
- **7 PivotCharts:** Employees by Department, Average Income by Department, Job Satisfaction by Department, and Attrition Rate by Department, Job Role, Business Travel and Experience.
- **Slicers:** Department and Gender, connected to all KPI cards and charts.

## Key results

| KPI | Value |
|---|---|
| Total Employees | 4,410 |
| Attrition Rate | 16.1% (711 leavers) |
| Average Monthly Income | 65,029 |
| Average Job Satisfaction | 2.73 / 4 |
| Average Performance Rating | 3.15 / 4 |

## Key insights

1. **The HR department's attrition (30.2%) is nearly double the company rate**, and HR is also the lowest-paid department.
2. **Early-career employees leave most:** 43.8% attrition for 0-2 years of total experience; 35.8% for ages 18-25.
3. **New joiners are at risk:** 29.8% attrition in the first 2 years at the company, accounting for 43% of all leavers.
4. **Frequent business travel is strongly associated with attrition:** 24.9% vs 8.0% for non-travellers. Frequent travellers are 18.8% of staff but 29% of leavers, and the pattern holds within departments.
5. **Senior research staff are at risk:** Research Directors have the highest role attrition (23.8%).

Satisfaction scores barely differ between departments (2.68–2.78), so pay, tenure and career stage are stronger signals than department-level satisfaction.

## Recommendations

1. **Strengthen onboarding and early-career support:** a structured 12–24 month mentorship and check-in programme for new joiners and employees aged 18-35.
2. **Review pay and workload in the HR department:** benchmark HR salaries and staffing levels.
3. **Reduce the burden of frequent travel:** rotate travel duties, use virtual meetings, and offer recovery time or allowances.
4. **Create retention plans for senior research roles:** stay interviews, career paths and succession planning for Research Directors.
5. **Track attrition drivers going forward:** collect overtime data and run exit interviews.

## Limitations

- **No overtime data** in the dataset, so business travel is used as an alternative workload indicator.
- **PerformanceRating has only two values (3 and 4)**, which limits its usefulness for explaining attrition.
- Missing survey answers are excluded from satisfaction averages.
- Findings show associations, not proven causes.

## Workbook structure

| Sheet | Contents |
|---|---|
| Dashboard | KPI cards, charts and slicers |
| Insights | Key insights and recommendations |
| CleanData | Final analysis-ready dataset (Power Query output + calculated columns) |
| Analysis | Workforce and satisfaction PivotTables |
| Attrition | Attrition PivotTables |
| KPI | KPI formulas and KPI PivotTable |
| Data Quality | Issues found and how they were handled |
| Field Logic | Calculated field definitions |
| ChartData | PivotTables feeding the dashboard charts |

Power Query steps can be viewed under **Data → Queries & Connections** (queries: EmployeeInfo, EmployeeSurvey, ManagerSurvey, HR_Clean).

## How to use

1. Open `HR_Analytics_Kevina.xlsx` in Microsoft Excel (desktop).
2. If the CSV files are in a different folder, update each query's source path in Power Query.
3. Click **Data → Refresh All**.
4. Use the **Department** and **Gender** slicers on the Dashboard to explore.
