# Data Analytics Pipeline: E-Commerce Marketing Campaign Data Cleaning

## Project Overview
This project targets the systemic extraction, transformation, and structural validation of an unrefined retail marketing dataset containing over 99,000 raw campaign logs. Raw data natively extracted from business environments is frequently compromised by structural anomalies, missing metrics, formatting inconsistencies, and indexing duplicate strings. 

To bridge the gap between raw backend logging and downstream business intelligence (BI) consumption, this project implements a two-tier data cleaning pipeline leveraging both **SQL (MySQL)** for structural data engineering and **Python (Pandas)** for programmatic deep-cleaning.

## Data Cleaning Architecture & Process

### Phase 1: Structural Setup & Staging (SQL / MySQL)
To preserve the absolute integrity of our source database, the data cleaning process initiates with database setup, schema replication, and the segregation of operational data:
* **Staging Table Isolation:** Created a parallel staging structure (`marketing_campaign_staging`) mimicking the primary raw export schema. This ensures all destructive formatting transformations occur safely outside the core ledger environment.
* **Duplicate Triage:** Implemented row-indexing algorithms across native composite keys (`Campaign_ID`, `Company`, `Date`) to catch overlapping backend server writes.
* **Schema Uniformity:** Configured baseline data types, ensuring financial fields, string labels, and volumetric trackers are normalized under strict uniform schemas.

### Phase 2: Programmatic Transformation & Imputation (Python / Pandas)
Once structured logs were systematically organized in MySQL, the staging layer was ingested into a Python environment for programmatic optimization via the Pandas library:
* **Handling Null Ratios:** Developed conditional filtering logic to capture and fix missing values. Numerical features (like target conversions and score rates) were dynamically imputed using median distribution weights to avoid statistical skewing.
* **Datetime Refinement:** Re-engineered multi-format text stamps into formalized `YYYY-MM-DD` ISO standards, resolving timeline calculation blockers.
* **Categorical String Alignment:** Normalized text fields (such as location labels, acquisition channels, and target sectors) by applying strict string stripping, case alignment (Title Case), and duplicate categorical consolidation.
* **Outlier Boundary Constraints:** Applied programmatic thresholding to evaluate extreme spikes in transactional spend and Return on Investment (ROI) metrics, filtering out recording glitches without eroding high-value variances.

## Data Quality Assurance & Validation Checks
The success of this data cleaning pipeline is validated against strict automated operational standards:
1. **Zero Null Records:** Verification script confirms all target analytical columns have a 100% complete data fill rate.
2. **Unique Index Enforcement:** Primary keys are evaluated to ensure a 0% duplication frequency across the global campaign array.
3. **Downstream Business Readiness:** The resulting structural dataset is systematically validated to perfectly match schema requirements for immediate deployment into analytics environments (such as Power BI dashboards or regression models).

## Technologies Utilized
* **Database Management System:** MySQL Workbench (SQL Data Definition and Manipulation Language)
* **Development Environment:** Anaconda Jupyter Notebook (Python 3)
* **Core Libraries Deployed:** NumPy, Pandas, Datetime
