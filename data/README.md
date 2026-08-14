# Dataset Documentation & Data Dictionary

## Overview & Lineage

The dataset in this repository was extracted directly from the Tableau Packaged Workbook extract (`federated.hyper`) embedded within [`Human Resources Analyst.twbx`](../tableau/Human%20Resources%20Analyst.twbx).

* **Dataset Name**: `HRDataset_v14.csv` (Recovered: `HRDataset_v14_recovered.csv`)
* **Total Records**: 311 rows
* **Total Features**: 36 columns
* **Data Nature**: **Synthetic / Academic HR Benchmark Dataset**
* **Origin**: Created by Dr. Rich Huebner and Dr. Carla Prichard for educational case studies, talent analytics modeling, and HR portfolio projects.

> [!NOTE]
> **Data Privacy & Synthetic Notice**: This dataset consists entirely of synthetic/fictional records created for academic and data visualization practice. Fictional employee names, IDs, and demographic values are included strictly for analytical demonstration. No real-world individuals or confidential corporate HR records are contained in this repository.

---

## Schema & Column Reference

| Column Name | Data Type | Tableau Role | Description | Null Count |
| :--- | :--- | :--- | :--- | :--- |
| `Employee_Name` | String | Dimension | Fictional name of employee (`Last, First Middle`) | 0 |
| `EmpID` | Integer | Dimension | Unique 5-digit employee identification number | 0 |
| `MarriedID` | Integer | Dimension | Binary marital indicator (`1` = Married, `0` = Single/Other) | 0 |
| `MaritalStatusID` | Integer | Dimension | Numeric code representing marital status (0–6) | 0 |
| `GenderID` | Integer | Dimension | Numeric code representing gender (`0` = Female, `1` = Male) | 0 |
| `EmpStatusID` | Integer | Dimension | Employment status category code (1–5) | 0 |
| `DeptID` | Integer | Dimension | Department identification code (1–6) | 0 |
| `PerfScoreID` | Integer | Dimension | Performance rating numeric code (1–4) | 0 |
| `FromDiversityJobFairID` | Integer | Dimension | Binary indicator if sourced from diversity job fair (`0` or `1`) | 0 |
| `Salary` | Integer | Measure | Annual employee compensation ($ USD) | 0 |
| `Termd` | Integer | Dimension | Binary termination flag (`1` = Terminated, `0` = Active) | 0 |
| `PositionID` | Integer | Dimension | Job position identification code (1–30) | 0 |
| `Position` | String | Dimension | Job title (e.g., `Production Technician I`, `Data Analyst`) | 0 |
| `State` | String | Dimension | US State of residence (primary: `MA`) | 0 |
| `Zip` | Integer | Dimension | Postal ZIP code | 0 |
| `DOB` | Date | Dimension | Date of Birth (`YYYY-MM-DD`) | 0 |
| `Sex` | String | Dimension | Biological sex (`F` = Female, `M` = Male) | 0 |
| `MaritalDesc` | String | Dimension | Marital status description (`Single`, `Married`, `Divorced`, etc.) | 0 |
| `CitizenDesc` | String | Dimension | Citizenship status description (`US Citizen`, `Eligible NonCitizen`, etc.) | 0 |
| `HispanicLatino` | String | Dimension | Self-reported Hispanic/Latino ethnicity indicator (`Yes`, `No`) | 0 |
| `RaceDesc` | String | Dimension | Self-reported racial demographic group | 0 |
| `DateofHire` | Date | Dimension | Official hiring date (`YYYY-MM-DD`) | 0 |
| `DateofTermination` | Date | Dimension | Official termination date (null for active staff) | 207 |
| `TermReason` | String | Dimension | Primary reason for termination (`N/A-StillEmployed` if active) | 0 |
| `EmploymentStatus` | String | Dimension | Status (`Active`, `Voluntarily Terminated`, `Terminated for Cause`) | 0 |
| `Department` | String | Dimension | Organizational department name | 0 |
| `ManagerName` | String | Dimension | Direct manager name | 0 |
| `ManagerID` | Float | Dimension | Direct manager numeric identifier (null for executive leadership) | 8 |
| `RecruitmentSource` | String | Dimension | Primary talent acquisition channel | 0 |
| `PerformanceScore` | String | Dimension | Performance review category (`Exceeds`, `Fully Meets`, `Needs Improvement`, `PIP`) | 0 |
| `EngagementSurvey` | Float | Measure | Annual employee engagement survey score (Scale: 1.00–5.00) | 0 |
| `EmpSatisfaction` | Integer | Measure | Employee self-reported satisfaction rating (Scale: 1–5) | 0 |
| `SpecialProjectsCount` | Integer | Measure | Number of special projects/stretch assignments completed | 0 |
| `LastPerformanceReview_Date` | Date | Dimension | Date of most recent performance review | 0 |
| `DaysLateLast30` | Integer | Measure | Number of late clock-in occurrences in the last 30 days | 0 |
| `Absences` | Integer | Measure | Total recorded unexcused absences during tenure | 0 |

---

## Data Extraction & Verification Method

The recovered dataset [`HRDataset_v14_recovered.csv`](./HRDataset_v14_recovered.csv) was extracted directly from the `.hyper` extract using the official Tableau Hyper API in Python:

```python
from tableauhyperapi import HyperProcess, Telemetry, Connection

with HyperProcess(telemetry=Telemetry.DO_NOT_SEND_USAGE_DATA_TO_TABLEAU) as hyper:
    with Connection(endpoint=hyper.endpoint, database="Data/.../federated.hyper") as connection:
        res = connection.execute_list_query('SELECT * FROM "Extract"."Extract"')
```

The extracted record count (311 rows) matches the distinct employee count in the Tableau workbook XML with 100% integrity.
