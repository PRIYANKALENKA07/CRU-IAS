# CRU-IAS — Crime Response Unit Intelligence & Analytics System

> An end-to-end crime data intelligence system built on FIR-level data 
> covering data pipeline, analytics, and an interactive browser-based dashboard.

---

## Project Journey

This project started as a **Power BI dashboard** built during a training
program on Karnataka Government crime data. After completing 2 months of
detailed documentation for the Power BI dashboard, I decided to take it
further — rebuilding the entire system from scratch with a custom Python
data pipeline and a self-built HTML dashboard, removing the dependency on
any paid BI tool.

The result is a fully independent, open-source intelligence system that
runs entirely without Power BI, Tableau, or any backend server.

---

## What is CRU-IAS?

CRU-IAS (Crime Response Unit — Intelligence & Analytics System) is a
personal data engineering and analytics project built on dummy FIR
(First Information Report) data modeled after Karnataka Government
crime records.

The system takes 7 raw data tables, cleans and joins them using Python,
and produces a single aggregated summary that powers an interactive
HTML dashboard — where you can select a police station and year and
instantly see total cases, disposed cases, and pending cases with charts.

---

## The Problem It Solves

Before this system, answering a simple question like:

> *"How many cyber crime cases are pending in Ashoknagar PS this year?"*

required manually joining multiple tables and writing custom queries
every single time. Nobody could answer that question quickly.

CRU-IAS does that automatically — in under two seconds.

---

## Key Finding

> **91% of cases in this dataset are still pending.**

This system helps police leadership spot which stations have the highest
backlog, which crime types are piling up, and where resources need to go.

---

## Dataset

| Detail | Value |
|---|---|
| Source | Karnataka Government (Dummy Data) |
| Time Period | 2020 – 2025 |
| Total Raw FIRs | 2,11,863 cases |
| Districts Covered | 45 |
| Police Stations | 50 |
| Raw Tables | 7 |
| Unique FIRs after cleaning | 1,40,585 |
| Final Dashboard Output | 9,453 aggregated rows |

**Raw tables included:**
Crime, Dispose, Act_Section, Accused, Chargesheet, PS_Unit, Victim

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data Pipeline | Python, Pandas, NumPy, Jupyter Notebook |
| Dashboard | HTML, CSS, JavaScript, Chart.js, SheetJS |
| Version Control | Git, GitHub |

---

## Project Structure
CRU-IAS
```plaintext
CRU-IAS/
│
├── notebooks/
│   └── 01_data_pipeline.ipynb    ← Full pipeline: clean, join, aggregate
│
├── data/
│   └── cru_aggregated.csv        ← Final pipeline output (dashboard input)
│
├── dashboard/
│   └── index.html                ← Self-contained analytics dashboard
│
└── README.md
```
## Power BI Dashboard File

📥 [Download Power BI File (.pbix)](https://drive.google.com/file/d/1C4Kw6QRmIPvkzhje-ipfluFQ2sBmQCIh/view?usp=drive_link)

## Phase 1 — Data Pipeline (Python + Pandas)

The pipeline transforms 7 raw CSV tables into one clean aggregated file.

**Steps:**

1. Load all 7 raw CSV tables into Pandas DataFrames
2. Drop junk columns (`Unnamed: 18`, `Unnamed: 19`), standardize column
   names, convert date columns to `datetime64` format
3. Extract `FIR_Year`, `FIR_Month`, `FIR_Month_Name` from `FIR_Date`
4. Create composite key `Fir_id + Unit_id` across Crime, Dispose, and
   Act tables to uniquely identify each FIR at each police station
5. Deduplicate Crime table from **2,11,863 rows → 1,40,585 unique FIRs**
6. Left join Dispose table → flag each FIR as `Is_Disposed` or
   `Is_Pending` based on whether a disposal date exists
7. Join primary Act Description per FIR → one crime type label per case
8. Aggregate by Police Station + Year + Month + Crime Type → compute
   Total Cases, Disposed Cases, Pending Cases, Pending Percentage
9. Fix act name inconsistencies (whitespace, `&` vs `and`, double spaces)
10. Export final `cru_aggregated.csv` — **9,453 rows, 100 unique act types**

---

## Phase 2 — Analytics Dashboard (HTML + JavaScript)

A self-contained, browser-based analytics dashboard with no backend,
no server, and no paid tool dependency.

**How it works:**

- User uploads `cru_aggregated.csv` or `.xlsx` directly in the browser
- SheetJS parses the file entirely client-side — no network request needed
- Select a **Police Unit** and **Year** → dashboard updates instantly
- All filtering, aggregation, and chart rendering happens in-memory

**Dashboard features:**

| Feature | Description |
|---|---|
| Grand Total Banner | Dataset-wide totals — all units, all years at a glance |
| KPI Cards | Total Cases, Pending Cases, Solved Cases, Pending Rate |
| Top 8 Act Types Chart | Horizontal bar chart of highest volume crime types |
| Year-wise Trend Line | Case volume trend for selected station across all years |
| All Units Comparison | Top 15 stations ranked by case volume for selected year |
| Act Type Breakdown Table | Per-act totals with High / Medium / Low pending status pill |

---

## Data Quality Issues Fixed

| # | Issue | Action Taken |
|---|---|---|
| 1 | 71,278 duplicate FIR rows in Crime table | Deduplicated on composite Key |
| 2 | Multiple act sections per FIR inflating counts | Took primary act per FIR only |
| 3 | Inconsistent act names (`&` vs `and`, double spaces) | Standardized using `.replace()` and `.str.strip()` |
| 4 | 1,814 FIRs with no act record | Filled as `'Unknown'` |
| 5 | BOM characters in CSV column names | Stripped during file parsing in dashboard |

---

## Why Not Power BI?

| | Power BI | CRU-IAS |
|---|---|---|
| Cost | Paid license required | Free — runs in any browser |
| Data prep | Manual every time | Automated Python pipeline |
| Portability | Requires Power BI Desktop | Single HTML file, runs anywhere |
| Customization | Limited to built-in visuals | Fully custom charts and logic |
| Offline use | Requires account | Works completely offline |

---

## What's Next

- [ ] Monthly trend line chart per station
- [ ] Pending percentage gauge visual
- [ ] District-level rollup view
- [ ] Top 5 backlog stations view
- [ ] Predictive model — forecast crime volume by station and month
- [ ] Automated pipeline scheduling

---

## Project Journey

| Phase | What was built | Time |
|---|---|---|
| Training Project | Power BI dashboard + 2 months of detailed documentation | Aug 2025 |
| CRU-IAS v1 | Python data pipeline + HTML dashboard + full technical documentation | Feb 2025 |

![Overview of the system ](https://github.com/PRIYANKALENKA07/CRU-IAS/blob/main/Overview/System%20Overview.png)
---

## Author

**Priyanka Lenka**
📧 priyankalenkabbs@gmail.com
🗓️ 2025


> *This project uses dummy data modeled 
> records and was built for learning and portfolio purposes.*
