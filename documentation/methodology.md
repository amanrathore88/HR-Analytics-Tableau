# Analytical Methodology & Technical Architecture

## End-to-End Workflow

The analytical process follows a structured, data-driven lifecycle:

```
[ Tableau .twbx Archive ]
          │
          ├──> Extract .hyper Database (311 Records, 36 Fields)
          │           │
          │           └──> Independent Python Verification (Pandas / Numpy)
          │
          ├──> Reverse-Engineer .twb XML (17 Sheets, 5 Dashboards, 12 Filter Actions)
          │           │
          │           └──> Formula Audit & Metric Lineage Mapping
          │
          └──> Dashboard Synthesis & Recruiter-Ready Portfolio Documentation
```

---

## 1. Data Ingestion & Extraction

1. **Packaged Workbook Extraction**: The `.hyper` extract embedded inside [`Human Resources Analyst.twbx`](../tableau/Human%20Resources%20Analyst.twbx) was decompressed and queried using the official `tableauhyperapi` library.
2. **Schema & Integrity Audit**: All 311 employee records and 36 attribute columns were validated against the Tableau XML datasource definitions. Record counts, null patterns, and categorical distributions were verified with 100% concordance.
3. **Data Privacy Check**: Confirmed that the underlying records originate from the academic benchmark synthetic HR dataset (`HRDataset_v14.csv`).

---

## 2. Calculated Field Engineering

Calculated fields in the Tableau workbook were extracted directly from the underlying XML definitions. Each calculated field was classified into:
* **Tableau Metadata Name**: The system-generated XML identifier (e.g., `Calculation_1422574578610319361`).
* **Display Caption**: User-facing pill label in the Tableau interface.
* **Original Tableau Formula**: The exact formula written in Tableau calculation editor.
* **Independent Verification**: Statistical re-computation in Python.
* **Methodological Distinction**: Clearly differentiating original student formulas from standard SHRM HR metrics.

---

## 3. Visualization Design & Chart Selection

The workbook utilizes functional, goal-oriented visual encoding:
* **Bar Charts (Horizontal & Vertical)**: Used for discrete categorical comparisons (Department sizes, Recruitment source yields, Termination reasons).
* **Donut / Pie Chart**: Applied to categorical workforce compositions (Gender ratio).
* **Line / Trend Charts**: Displayed temporal trajectories over hire and termination years.
* **Scatter & Circle Plots**: Utilized for exploratory multi-variable distributions (Performance vs. Review Year, Manager vs. Performance).
* **Text / Shape Tables**: Implemented for individual talent leaderboards and structured cross-tabulations.

---

## 4. Interactive Dashboard Architecture & Filter Actions

The workbook connects 17 worksheets across 5 thematic dashboards utilizing **12 Tableau Filter Actions**:
* **Cross-filtering**: Clicking on a department bar in Dashboard 1 dynamically filters the adjacent age histogram and gender breakdown.
* **Drill-down Actions**: Selecting a specific recruitment channel or termination reason filters time-series trends and position breakdowns.
* **Target Actions**: Configured to pass selected dimension keys across sheets without requiring external parameter overhead.
