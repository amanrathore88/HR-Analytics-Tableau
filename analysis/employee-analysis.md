# Workforce & Demographic Analysis

## 1. Demographic Profile

### Gender Distribution (Sheet 2)
![Sheet 2: Gender Distribution](../screenshots/sheets/sheet-02-gender-distribution.png)

* **Female (`Gender ID: 0`)**: 176 employees (**56.59%**)
* **Male (`Gender ID: 1`)**: 135 employees (**43.41%**)
* **Total**: 311 employees

### Age Bracket Breakdown (Sheet 1)
![Sheet 1: Age Distribution](../screenshots/sheets/sheet-01-age-distribution.png)

In the Tableau workbook, employee age is binned into 5-year step intervals (`Age (bin)`: 30, 35, 40, 45, 50, 55, 60, 65, 70, 75) and evaluated alongside `SUM(Count)`, `SUM(DaysLateLast30)`, and `SUM(Age)`:
* **Age 30**: 3 employees
* **Age 35**: 59 employees
* **Age 40**: 79 employees — *Peak Demographic Cohort*
* **Age 45**: 61 employees
* **Age 50**: 46 employees
* **Age 55**: 32 employees
* **Age 60**: 17 employees
* **Age 65**: 4 employees
* **Age 70**: 8 employees
* **Age 75**: 2 employees

---

## 2. Departmental Breakdown (Sheet 3)

![Sheet 3: Department Distribution](../screenshots/sheets/sheet-03-department-distribution.png)

| Department | Headcount | % of Total | Active Count | Terminated Count |
| :--- | :--- | :--- | :--- | :--- |
| **Production** | 209 | 67.20% | 126 | 83 (39.71% attrition) |
| **IT/IS** | 50 | 16.08% | 40 | 10 (20.00% attrition) |
| **Sales** | 31 | 9.97% | 26 | 5 (16.13% attrition) |
| **Software Engineering** | 11 | 3.54% | 7 | 4 (36.36% attrition) |
| **Admin Offices** | 9 | 2.89% | 7 | 2 (22.22% attrition) |
| **Executive Office** | 1 | 0.32% | 1 | 0 (0.00% attrition) |

---

## 3. Compensation & Pay Equity Analysis (Sheet 17)

![Sheet 17: Pay Equity Analysis](../screenshots/sheets/sheet-17-pay-equity.png)

* In Sheet 17, total payroll is evaluated as `SUM(Salary)` stacked by `Gender ID` across departments (Total Organizational Payroll: **$21,465,433**).
* **Production Department**: Female payroll accounts for **$7,512,173** (59.8%) of the $12,530,291 department total, reflecting the high representation of female technicians (126 Female vs. 83 Male).
* **IT/IS Department**: Total payroll is $4,853,232 (22 Female staff totaling $2,081,046 vs. 28 Male staff totaling $2,772,186).
* **Executive Office**: Single female executive with an annual compensation of $250,000.
