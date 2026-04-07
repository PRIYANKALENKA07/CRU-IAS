# CRU-IAS — Crime Response Unit Intelligence & Analytics System

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Pipeline-lightgrey?style=flat&logo=pandas)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange?style=flat)
![License](https://img.shields.io/badge/License-Academic-green?style=flat)

> A end-to-end crime data intelligence system built on FIR-level data from the Crime Response Unit (CRU) — covering data pipeline, analytics dashboard, and predictive modeling.

---

## 🗂️ Project Overview

The **Crime Response Unit (CRU)** collects FIR (First Information Report) level data across **45 districts and 50 police stations** spanning **2020–2025** (~5 years, 2,11,863 cases).

This system transforms that raw data into actionable intelligence through three phases:

| Phase | Description | Status |
|-------|-------------|--------|
| **Phase 1** | Data Pipeline — clean, join & aggregate raw tables | 🔄 In Progress |
| **Phase 2** | Analytics Dashboard — interactive HTML system with charts | ⏳ Planned |
| **Phase 3** | Predictive Model — ML-based crime forecasting system | ⏳ Planned |

---

## 📁 Repository Structure
CRU-IAS/
├── data/                        # Raw source tables (CSV)
│   ├── crime.csv                # Core FIR data (2,11,863 records)
│   ├── dispose.csv              # Case disposal records (17,660 records)
│   ├── act_section.csv          # Crime type / law sections (3,49,029 records)
│   └── ps_unit.csv              # Police station master data (1,856 records)
├── notebooks/
│   └── 01_data_pipeline.ipynb  # Phase 1 — data pipeline & analysis
├── output/
│   └── cru_aggregated.csv      # Final aggregated output (pipeline output)
├── docs/
│   └── CRU_Analytics_Documentation.docx  # Power BI dashboard documentation
├── .gitignore
└── README.md
---

## 📊 Data Sources

| Table | Records | Columns | Description |
|-------|---------|---------|-------------|
| `crime.csv` | 2,11,863 | 18 | Core FIR details — location, date, crime type, stage |
| `dispose.csv` | 17,660 | 5 | Case disposal info — disposal date and type |
| `act_section.csv` | 3,49,029 | 6 | Law sections — crime classification and description |
| `ps_unit.csv` | 1,856 | 4 | Police station master — names and coordinates |

**Time Range:** January 2020 – January 2025  
**Geography:** 45 Districts, 50 Police Stations

---

## ⚙️ Phase 1 — Data Pipeline

The notebook `01_data_pipeline.ipynb` performs the following steps:

1. **Load & Clean** — load all raw tables, drop junk columns, standardize join keys
2. **Join Dispose** — flag each FIR as `Disposed` or `Pending` based on `Dispose_Date`
3. **Join Act_Section** — bring in `Act_Description` (crime type) for each FIR
4. **Build Master Table** — one clean row per FIR with all key fields
5. **Aggregate** — group by `UnitName + Month + Act_Description`, count cases
6. **Export** — save `cru_aggregated.csv` to `output/`

---

## 🛠️ Tech Stack

- **Python 3.10+**
- **Pandas** — data manipulation and pipeline
- **NumPy** — calculations
- **Jupyter Notebook** — interactive analysis and documentation
- **Power BI** — original dashboard (see `docs/`)

---

## 👩‍💻 Author

**Priyanka Lenka**  
Data Analyst — Training Project  
[GitHub](https://github.com/PRIYANKALENKA07)

---

*This project is part of a structured learning program in data analytics and predictive modeling.*
