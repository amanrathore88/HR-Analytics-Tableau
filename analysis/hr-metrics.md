# Key HR Metrics & Calculation Audit

This document outlines the core HR metrics, formulas, independent recalculations, and methodological nuances identified in the project.

---

## Metric Comparison: Original Workbook vs. Standard HR Formulations

| HR Metric | Original Tableau Formula | Original Metric Meaning | Standard SHRM / HR Formula |
| :--- | :--- | :--- | :--- |
| **Turnover Rate** | `IF ISNULL([DateofTermination]) THEN 0 ELSE 1 END` | **Annual Termination Count** ($\sum = 104$) | $\frac{\text{Terminations}}{\text{Average Headcount}} \times 100$ |
| **Hiring Rate** | `COUNTD([EmpID])` | **Annual New Hire Volume** ($\sum = 311$) | $\frac{\text{New Hires}}{\text{Total Headcount}} \times 100$ |
| **Time to Fill** | `DATEDIFF('day', [DOB], [DateofHire])` | **Age at Hire (in Days)** | $\text{Offer Date} - \text{Requisition Open Date}$ |
| **Headcount** | `SUM(Count)` where `Count = 1` | **Total Headcount** ($311$) | Total active + terminated records in cohort |
| **Average Engagement** | `AVG([EngagementSurvey])` | **Mean Survey Rating** ($4.11 / 5.0$) | Weighted mean of employee survey responses |

---

## 1. Turnover & Attrition Breakdown

* **Total Terminations**: 104 employees (33.44% cumulative attrition across all historical hiring cohorts).
* **Voluntary Terminations**: 88 employees (84.6% of all exits).
* **Terminated for Cause**: 16 employees (15.4% of all exits).

### Annual Termination Distribution:
```
2011:  █████████ 9
2012:  ██████████████ 14
2013:  ████████████████ 16
2014:  █████████████████████ 21 (Peak)
2015:  █████████████████████ 21 (Peak)
2016:  ██████████████ 14
2017:  ██████ 6
2018:  ███ 3
```

---

## 2. Hiring Volume Trends

* **Total Recorded Hires**: 311 distinct employees (`COUNTD([EmpID]) = 311`).
* **Peak Hiring Cohort**: 2011 represented the primary organizational expansion year with **77 new hires** (24.8% of total workforce), followed by 2014 (56 hires) and 2013 (43 hires).

---

## 3. Time to Fill & Age-at-Hire Proxy

* **Tableau Calculation**: `DATEDIFF('day', [DOB], [DateofHire])`
* **Analytical Note**: In standard HR analytics, *Time to Fill* calculates the days between opening a requisition and candidate offer acceptance. In the original student workbook, this metric was implemented as the difference between Date of Birth and Date of Hire, effectively measuring employee tenure age at entry.
* **Average Age at Hire by Functional Level**:
  * Executive & Director Roles (e.g., *Director of Sales*, *BI Director*): 44.5–48.1 years
  * Middle Management (e.g., *Production Manager*, *IT Manager*): 37.2–43.8 years
  * Entry/Technician Roles (e.g., *Production Technician I*, *IT Support*): 30.2–34.1 years

---

## 4. Employee Engagement & Satisfaction

* **Engagement Survey Scale**: 1.00 to 5.00
  * **Mean Score**: 4.11
  * **Median Score**: 4.28
  * **25th Percentile**: 3.69
  * **75th Percentile**: 4.70
  * **Standard Deviation**: 0.79
* **Correlation with Performance**:
  * Employees rated *Exceeds* averaged **4.45** on engagement.
  * Employees on a *PIP* (Performance Improvement Plan) averaged **2.22** on engagement.
