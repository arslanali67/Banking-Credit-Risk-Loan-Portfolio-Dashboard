# Banking-Credit-Risk-Loan-Portfolio-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/your-report-id/ReportSection

---

## Problem Statement

This dashboard helps banking and financial institutions gain a comprehensive understanding of their loan portfolio and associated credit risk. It enables risk analysts and decision-makers to identify which borrower segments, employment types, and loan purposes are driving default rates — and how those risks have evolved over time (2013–2018).

Through detailed ratings, demographic breakdowns, and financial metrics, the dashboard surfaces critical improvement areas. Since unemployed borrowers show the highest default rate (3.39%) and the overall portfolio has exhibited a rising risk trend heading into 2018 (11.60%), institutions can use these insights to refine lending criteria, improve risk scoring models, and proactively manage portfolio exposure.

Furthermore, since average default rates peaked at 11.75% in 2016 and have not returned to their 2014 low of 11.50%, institutions must investigate the structural factors — such as employment type mix and income bracket distribution — contributing to sustained elevated risk.

---

### Steps followed

- **Step 1 :** Load data into Power BI Desktop. The dataset is a CSV file (`Loan_default.csv`) containing **255,347 loan records**.

- **Step 2 :** Open Power Query Editor. Under the **View** tab in the **Data Preview** section, enable **"Column Distribution"**, **"Column Quality"**, and **"Column Profile"** options to inspect data health.

- **Step 3 :** Since by default column profiling is applied to only the first 1,000 rows, change the setting to **"Column profiling based on entire dataset"** to get accurate quality metrics across all 255,347 records.

- **Step 4 :** During data profiling, it was observed that most columns were clean with no errors. Minor null values were identified in financial-related columns and handled appropriately in downstream calculations.

- **Step 5 :** In the **Report View**, a theme was applied under the **View** tab to establish a consistent visual identity (mauve/dusty-rose color palette) across all three report pages.

- **Step 6 :** A **Calculated Column** was created to segment borrowers into meaningful age groups for demographic analysis.

  Following DAX expression was written for the same:

        Age Group =
        if(Loan_default[Age]<=25, "Teen",
        if(Loan_default[Age]<=40, "Adults",
        if(Loan_default[Age]<=65, "Middle Age Adults",
        "Senior Citizens")))



- **Step 7 :** A new **Measure** was created to calculate the total count of loan records.

  Following DAX expression was written for the same:

        Count of Loans = COUNT(Loan_default[LoanID])

  A **Card Visual** was used to display this KPI prominently on the overview page.



- **Step 8 :** A new **Measure** was created to calculate the total loan amount disbursed across the portfolio.

  Following DAX expression was written for the same:

        Sum of LoanAmount = SUM(Loan_default[LoanAmount])

  A **Card Visual** was used to represent total loan volume.

  

- **Step 9 :** **Page 1 — Loan Default & Overview** was built with the following visuals:
  - **Area/Line Chart** — Loan Amount by Purpose (Home, Business, Education, Auto, Other)
  - **Step Line Chart** — Average Income by Employment Type (Full-time, Self-employed, Part-time, Unemployed)
  - **Step Line Chart** — Default Rate (%) by Employment Type
  - **Area Chart** — Average Loan Amount by Age Groups
  - **Area Chart** — Default Rate (%) by Year (2013–2018)

- **Step 10 :** **Page 2 — Applicant Demographics & Financial Profile** was built with the following visuals:
  - **Line Chart** — Median Loan by Credit Score Category (Low, Mid High, Very Low, High)
  - **Donut Chart** — Average Loan by High Credit Scorers segmented by Age Group and Marital Status
  - **Line Chart** — Total Loan (Adults) by Credit Score Category
  - **Clustered Bar Chart** — Total Loan (Middle Age Adults) by Mortgage and Dependents
  - **Line Chart** — Number of Loans by Education Level (Bachelor's, High School, Master's, PhD)

- **Step 11 :** **Page 3 — Financial Risk Matrices** was built with the following advanced visuals:
  - **Waterfall/Step Line Chart** — YoY Loan Amount Change by Year
  - **Waterfall/Step Line Chart** — YoY Default Loan Change by Year
  - **Marimekko/Matrix Chart** — YTD Loan Amount by Credit Score Categories and Marital Status
  - **Decomposition Tree** — Breakdown of Sum of Loan Amount by **Income Bracket** → **Employment Type**, filtered to High Income segment

- **Step 12 :** **Visual-Level Filters (Slicers)** were added across pages for interactive filtering by:
  - Employment Type
  - Credit Score Category
  - Marital Status
  - Age Group
  - Income Bracket

- **Step 13 :** In the **Report View**, under the **Insert** tab, **Text Boxes** were added to each page header. A consistent banner with the page title was applied using a rectangle shape, creating a unified dashboard header design.

- **Step 14 :** A **Default Rate (%)** measure was calculated using conditional logic to express the proportion of defaulted loans within each segment, enabling the default rate visuals across all three pages.

- **Step 15 :** **YoY (Year-over-Year) measures** were created using DAX `CALCULATE` and `DATEADD` functions to power the Financial Risk Matrices page — tracking both loan volume growth and default loan fluctuation on an annual basis from 2013 through 2018.

- **Step 16 :** The report was published to **Power BI Service** for sharing and scheduled refresh.

  

---

# Snapshot of Dashboard (Power BI Service)

### Page 1 — Loan Default & Overview



### Page 2 — Applicant Demographics & Financial Profile



### Page 3 — Financial Risk Matrices


---

# Report Snapshot (Power BI Desktop)

### Page 1 — Loan Default & Overview


### Page 2 — Applicant Demographics & Financial Profile


### Page 3 — Financial Risk Matrices


---

# Insights

A three-page report was created on Power BI Desktop and published to Power BI Service.

The following inferences can be drawn from the dashboard:

---

### [1] Total Portfolio Scale

   **Total Loan Records Analyzed = 255,347**

   The portfolio spans six years (2013–2018), covering borrowers across all employment types, income brackets, education levels, and age groups — making it a robust dataset for credit risk modelling.

---

### [2] Default Rate Trends (2013–2018)

   | Year | Default Rate (%) |
   |------|-----------------|
   | 2013 | 11.62 |
   | 2014 | 11.50 *(lowest)* |
   | 2015 | 11.70 |
   | 2016 | 11.75 *(peak)* |
   | 2017 | 11.50 |
   | 2018 | 11.60 |

   - Default rates **peaked in 2015–2016**, suggesting a period of heightened portfolio stress likely tied to macroeconomic conditions.
   - Rates **improved in 2017** but began climbing again in 2018 — signalling a **renewed risk uptrend** that warrants monitoring.
   - The institution must investigate risk underwriting practices during 2015–2016 to prevent a similar escalation cycle.

---

### [3] Loan Volume by Purpose

   | Purpose | Loan Volume |
   |---------|------------|
   | Home | 6,545M *(highest)* |
   | Business | 6,522M |
   | Education | 6,511M |
   | Auto | 6,501M |
   | Other | 6,498M |

   - **Home loans** represent the largest loan category by volume, closely followed by Business loans.
   - The distribution across purposes is relatively balanced, suggesting a diversified portfolio without extreme concentration risk in any single purpose category.

---

### [4] Default Rate by Employment Type

   | Employment Type | Default Rate (%) |
   |----------------|-----------------|
   | Unemployed | 3.39 *(highest risk)* |
   | Part-time | 3.01 |
   | Self-employed | 2.86 |
   | Full-time | 2.36 *(lowest risk)* |

   - **Unemployed borrowers** carry the highest default risk at 3.39% — nearly **44% higher** than full-time employees.
   - **Full-time employees** are the most reliable repayers, with the lowest default rate of 2.36%.
   - Lending policies should apply stricter income verification and higher risk premiums for unemployed and part-time borrowers.

---

### [5] Average Income by Employment Type

   | Employment Type | Average Income |
   |----------------|---------------|
   | Full-time | 82,890 *(highest)* |
   | Self-employed | 82,447 |
   | Part-time | 82,389 |
   | Unemployed | 82,272 *(lowest)* |

   - Average income is relatively consistent across employment types, with only marginal differences — suggesting that income alone is not the primary differentiator of default risk; **employment stability** is a stronger predictor.

---

### [6] Average Loan Amount by Age Group

   | Age Group | Average Loan Amount |
   |-----------|-------------------|
   | Adults (≤40) | 127,901 *(highest)* |
   | Middle Age Adults (≤65) | 127,459 |
   | Senior Citizens (>65) | 127,355 |
   | Teen (≤25) | 126,674 *(lowest)* |

   - **Adults (25–40)** take out the largest average loans, likely driven by major life purchases (homes, businesses).
   - **Teens** borrow the least on average, consistent with early-career financial profiles.

---

### [7] Credit Score & Loan Relationship

   | Credit Score Category | Median Loan Amount |
   |----------------------|-------------------|
   | Low | 128,397 *(highest)* |
   | Mid High | 127,764 |
   | Very Low | 127,515 |
   | High | 127,149 *(lowest)* |

   - Counterintuitively, borrowers with **lower credit scores** tend to be approved for slightly higher median loan amounts — this may reflect secured or collateral-backed products targeted at subprime segments and warrants further review.
   - **High credit score** borrowers carry the lowest median loan amounts, possibly due to more conservative personal borrowing behaviour.

---

### [8] Loans by Education Level

   | Education Level | Number of Loans |
   |----------------|----------------|
   | Bachelor's | 64,366 *(most)* |
   | High School | 63,903 |
   | Master's | 63,541 |
   | PhD | 63,537 *(least)* |

   - **Bachelor's degree holders** represent the largest segment of loan applicants, indicating the core borrower demographic.
   - The distribution across education levels is relatively even, suggesting education alone is not a strong segmentation driver.

---

### [9] YoY Loan & Default Volume Changes

   - **YoY Loan Amount** showed a significant drop in 2014 (-1.53) before recovering strongly in 2015 (+1.30) and reaching its highest growth in 2018 (+1.73).
   - **YoY Default Loans** mirrored a similar volatile pattern — falling sharply in 2014 (-2.6) and 2017 (-2.8), but surging in 2015 (+2.7) and 2018 (+1.9).
   - The **2018 upswing in both loan volume and defaults** is a critical signal for risk teams to stress-test current portfolios.

---

### [10] Income Bracket & Employment Type Decomposition

   | Income Bracket | Total Loan Amount |
   |---------------|-----------------|
   | High Income | 21.73bn |
   | Medium Income | 7.21bn |
   | Low Income | 3.63bn |

   Within the High Income segment (32.58bn total), loan amounts are **evenly distributed** across Full-time (5.44bn), Part-time (5.44bn), and Self-employed (5.43bn) employment types — demonstrating that high-income borrowers are well-represented regardless of employment type.
