# Tableau Calculated Fields & Formula Reference

This document provides a technical audit of all calculated fields extracted directly from the Tableau workbook XML (`Human Resources Analyst.twb`).

---

## Calculated Fields Inventory

| # | Field Caption | XML Identifier | Original Tableau Formula | Data Type | Role | Primary Usage |
| :- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | **Count** | `Calculation_1635651135752892417` | `1` | Integer | Measure | Record counter for headcount aggregations |
| 2 | **Age** | `Calculation_1635651135733358592` | `DATEDIFF('year', [DOB], TODAY())` | Integer | Measure | Dynamic employee age calculation in years |
| 3 | **Age (bin)** | `Age (bin)` | Binning on `[Age]` | Integer | Dimension | 10-year demographic age brackets for histograms |
| 4 | **Turnover Rate** | `Calculation_1422574578610319361` | `IF ISNULL([DateofTermination]) THEN 0 ELSE 1 END` | Integer | Measure | Binary termination flag (summed for total exits) |
| 5 | **Hiring Rate ** | `Calculation_1422574578612596738` | `COUNTD([EmpID])` | Integer | Measure | Distinct count of employee IDs per hire year |
| 6 | **Time to Fill** | `Calculation_1422574578613706755` | `DATEDIFF('day', [DOB], [DateofHire])` | Integer | Measure | Age in days at hire (dataset proxy) |
| 7 | **Is Terminated** | `Calculation_1422574578659508229` | `IF ISNULL([DateofTermination]) THEN 0 ELSE 1 END` | Integer | Measure | Indicator flag used in predictive exploration |

---

## Detailed Formula Analysis & Methodological Notes

### 1. `Count`
* **Formula**: `1`
* **Purpose**: Assigns a static constant value of 1 to every row to facilitate flexible `SUM(Count)` aggregations across various visual dimensions without relying on `COUNT([EmpID])`.
* **Total Aggregation**: $\sum = 311$ total records.

---

### 2. `Age` & `Age (bin)`
* **Formula**: `DATEDIFF('year', [DOB], TODAY())`
* **Purpose**: Computes employee age by calculating the date difference in years between Date of Birth (`DOB`) and current execution date.
* **Workbook Implementation**: Fed directly into a Tableau Bin (`Age (bin)`) with a step size of 10 years to generate demographic frequency distributions (Sheet 1).
* **Observed Distribution**: Median employee age is 44 years; range spans from early 30s to early 70s.

---

### 3. `Turnover Rate`
* **Formula**: `IF ISNULL([DateofTermination]) THEN 0 ELSE 1 END`
* **Tableau Usage**: Placed on Rows shelf in Sheet 4 as `SUM(Turnover Rate)` across `YEAR(DateofTermination)`.
* **Methodological Distinction**:
  * *Original Tableau Implementation*: This formula functions as a **binary termination indicator flag** (`0` = Active, `1` = Terminated). When summed in Tableau, it calculates the **total count of departures** (104 employees total).
  * *Standard HR Definition*: A standard HR Turnover Rate is typically calculated as:
    $$\text{Turnover Rate (\%)} = \left( \frac{\text{Number of Terminations}}{\text{Average Headcount}} \right) \times 100$$
  * *Preservation Note*: In this project documentation, we preserve the original formula and visual output exactly as authored, while explicitly noting that it represents annual termination counts.

---

### 4. `Hiring Rate `
* **Formula**: `COUNTD([EmpID])`
* **Tableau Usage**: Placed on Rows shelf in Sheet 6 across `YEAR(DateofHire)`.
* **Methodological Distinction**:
  * *Original Tableau Implementation*: Computes the **count of distinct new hires** per calendar year (e.g., peak of 77 hires in 2011).
  * *Standard HR Definition*: A standard HR Hiring Rate is calculated as:
    $$\text{Hiring Rate (\%)} = \left( \frac{\text{Total New Hires}}{\text{Total Headcount}} \right) \times 100$$
  * *Preservation Note*: Documented faithfully as the annual hiring volume metric used in the workbook.

---

### 5. `Time to Fill`
* **Formula**: `DATEDIFF('day', [DOB], [DateofHire])`
* **Tableau Usage**: Placed on Rows shelf in Sheet 8 grouped by `Position`.
* **Methodological Distinction**:
  * *Original Tableau Implementation*: Calculates the day difference between `DOB` (Date of Birth) and `DateofHire`, representing the **employee's age in days at the time they were hired** (~11,000 to ~18,000 days).
  * *Standard HR Definition*: Time to Fill measures recruiting cycle speed:
    $$\text{Time to Fill} = \text{Date of Job Offer Acceptance} - \text{Date Job Requisition Opened}$$
  * *Root Cause / Context*: The synthetic benchmark dataset did not contain a `JobPostingDate` or `RequisitionDate` column; this formula served as an applied date calculation in the original college project.
  * *Preservation Note*: Preserved exactly as constructed in the original workbook without alteration.

---

### 6. `Is Terminated`
* **Formula**: `IF ISNULL([DateofTermination]) THEN 0 ELSE 1 END`
* **Tableau Usage**: Used in Sheet 16 for exploratory cross-tabulation of performance ratings and engagement scores against termination status.
