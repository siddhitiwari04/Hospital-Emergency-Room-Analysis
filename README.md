# Hospital Emergency Room (ER) Performance & Patient Outcomes Analysis

![Project Status: Completed](https://img.shields.io/badge/Project%20Status-Completed-success)
![Tech Stack: Power BI | Python | SQL](https://img.shields.io/badge/Tech%20Stack-Power%20BI%20%7C%20Python%20%7C%20SQL-blue)
![Domain: Healthcare Analytics](https://img.shields.io/badge/Domain-Healthcare%20Analytics-red)

A comprehensive end-to-end data analytics and business intelligence project designed to evaluate emergency room operational efficiency, patient throughput bottlenecks, demographic patterns, and clinical satisfaction scores. This repository contains the data pipeline, data architecture, exploratory analysis, and interactive dashboard documentation engineered to transform raw clinical admission logs into executive-ready healthcare insights.

---

## Table of Contents
1. [Executive Summary & Business Problem](#executive-summary--business-problem)
2. [Project Objectives](#project-objectives)
3. [Repository Structure](#repository-structure)
4. [Dataset Architecture & Schema](#dataset-architecture--schema)
5. [Key Performance Indicators (KPIs)](#key-performance-indicators-kpis)
6. [Dashboard Architecture & Core Insights](#dashboard-architecture--core-insights)
   - [1. Executive Operational Overview](#1-executive-operational-overview)
   - [2. Patient Demographics & Cohort Analysis](#2-patient-demographics--cohort-analysis)
   - [3. Departmental Referrals & Satisfaction Deep-Dive](#3-departmental-referrals--satisfaction-deep-dive)
7. [Technical Methodology & BI Implementation](#technical-methodology--bi-implementation)
8. [Strategic Operational Recommendations](#strategic-operational-recommendations)
9. [Installation & Usage Instructions](#installation--usage-instructions)

---

## Executive Summary & Business Problem

Emergency Departments (EDs) operate in high-pressure, resource-constrained environments where operational delays directly degrade clinical outcomes and patient satisfaction. Hospital leadership frequently faces critical challenges regarding **patient wait time escalation**, **unpredictable admission surges**, and **departmental referral bottlenecks**.

This project establishes an empirical, data-driven framework to evaluate emergency room operations using historical clinical records. By isolating key operational drivers, the project bridges the gap between raw healthcare logs and administrative decision-making, providing actionable recommendations to reduce patient wait times, optimize staffing schedules, and improve patient care quality.

---

## Project Objectives

The primary objective of this project is to analyze historical patient admission logs from the Hospital Emergency Department to uncover structural bottlenecks, evaluate throughput efficiency, and identify key drivers of patient satisfaction and clinical outcomes. 

By leveraging advanced business intelligence and data analytics methodologies, this project aims to transition raw clinical data into actionable strategies for hospital leadership through the following core targets:

### 1. Operational Throughput & Wait Time Optimization
* **Identify Bottlenecks:** Quantify and map patient wait times across different admission hours, shifts, and days of the week to pinpoint peak congestion windows.
* **Shift Analysis:** Evaluate how staffing transitions (particularly during evening peak hours between 16:00 and 21:00) impact triage velocity and initial consultation delays.

### 2. Clinical Acuity & Resource Allocation
* **Referral Stream Mapping:** Analyze patient volume distributions across specialized departmental referrals (General Practice, Orthopedics, Physiotherapy) to align clinical staffing with demand.
* **Admission Flag Tracking:** Monitor inpatient escalation rates (`Patient Admission Flag = TRUE`) to understand clinical acuity trends and assist bed-management workflows in forecasting inpatient admission surges.
* **Case Management Intensity:** Evaluate the resource demands of high-complexity patient cohorts requiring dedicated Case Management (`Patients CM = 1`), particularly within geriatric populations (aged 65+).

### 3. Patient Experience & Quality of Care Improvement
* **Satisfaction Correlation:** Establish mathematical correlations between elapsed wait times and self-reported Patient Satisfaction Scores (1–10 scale) to isolate operational drivers of dissatisfaction.
* **Threshold Detection:** Identify critical wait-time thresholds (such as the observed "45-minute drop-off") where patient sentiment significantly degrades, enabling the creation of automated service-recovery protocols.

### 4. Demographic & Equity Slicing
* **Cohort Profiling:** Investigate how operational metrics vary across patient demographic profiles (Age, Gender, and Race) to ensure equitable care delivery and tailor specialized triage pathways for vulnerable groups (e.g., pediatric and geriatric patients).

---

## Repository Structure

```text
├── dashboards/
│   ├── executive_overview.png           # Executive KPI & throughput dashboard
│   ├── demographics_analysis.png        # Patient cohort & acuity breakdown
│   └── satisfaction_deep_dive.png       # Referral & satisfaction correlation analysis
├── data/
│   └── Hospital ER_Data.csv             # Cleaned clinical encounter dataset
├── scripts/
│   └── er_data_cleaning.py              # Python preprocessing & validation script
└── README.md                            # Project documentation
```

---

## Dataset Architecture & Schema

The analysis is built upon granular clinical encounter logs from `Hospital ER_Data.csv`. The dataset includes administrative timestamps, demographic attributes, clinical triage flags, and patient feedback ratings.

| Field Name | Data Type | Description |
| :--- | :--- | :--- |
| `Patient Id` | String | Unique alphanumeric identifier for each patient encounter (e.g., `145-39-5406`). |
| `Patient Admission Date` | DateTime | Timestamp indicating date and time when the patient entered the ER triage system. |
| `Patient First Initial` / `Last Name` | String | De-identified demographic identifiers. |
| `Patient Gender` | Categorical | Biological gender classification (`M`, `F`). |
| `Patient Age` | Integer | Patient age in years at the time of admission (ranges from pediatric to geriatric cohorts). |
| `Patient Race` | Categorical | Ethnic demographic classification (White, African American, Asian, Native American/Alaska Native, etc.). |
| `Department Referral` | Categorical | Specialty department to which the patient was directed (`General Practice`, `Orthopedics`, `Physiotherapy`, or `None`). |
| `Patient Admission Flag` | Boolean | Indicates whether the ER visit escalated into an inpatient hospital admission (`TRUE` or `FALSE`). |
| `Patient Satisfaction Score` | Integer (1–10)| Post-visit survey rating evaluating the patient's care experience (contains null values for non-respondents). |
| `Patient Waittime` | Integer | Total elapsed duration in minutes from ER arrival to initial physician or nursing consultation. |
| `Patients CM` | Binary (0/1) | Clinical Case Management flag indicating complex comorbidity tracking or specialized social work involvement. |

---

## Key Performance Indicators (KPIs)

The BI dashboard framework evaluates performance through four primary operational pillars:

1. **Average Wait Time (Minutes):** The core operational efficiency metric, tracked across temporal shifts (morning, evening, night) and patient complexity tiers.
2. **Inpatient Admission Rate (%):** The proportion of total ER encounters resulting in hospital admission (`Admission Flag = TRUE`), serving as a proxy for clinical acuity.
3. **Net Satisfaction Rating:** Average patient feedback score scaled out of 10, monitored to detect service quality degradation across specific departments or shifts.
4. **Case Management Ratio (%):** The percentage of active ER encounters requiring dedicated Case Management (`Patients CM = 1`), identifying high-resource patient cohorts.

---

## Dashboard Architecture & Core Insights

### 1. Executive Operational Overview
* **Objective:** Provide hospital executives with an immediate assessment of patient volume, throughput velocity, and overall system load.
* **Visual Reference:** `![Executive Overview](dashboards/executive_overview.png)`
* **Key Findings:**
  * **Peak Congestion Windows:** Patient inflow consistently peaks between 16:00 and 21:00, correlating with a significant increase in average wait times during evening shift handoffs.
  * **Acuity Distribution:** Approximately 45–50% of arriving patients require formal hospital admission, indicating a moderate-to-high acuity patient population that necessitates streamlined bed-management workflows.

### 2. Patient Demographics & Cohort Analysis
* **Objective:** Examine how age, gender, and racial demographics interact with clinical outcomes and resource utilization.
* **Visual Reference:** `![Demographics Analysis](dashboards/demographics_analysis.png)`
* **Key Findings:**
  * **Geriatric Resource Intensity:** Patients aged 65+ exhibit significantly higher Case Management involvement (`Patients CM = 1`) and longer average stay durations compared to adult and pediatric cohorts.
  * **Pediatric Volume Trends:** Pediatric admissions (<18 years) show distinct weekend volume spikes, primarily presenting with general practice and orthopedic needs.

### 3. Departmental Referrals & Satisfaction Deep-Dive
* **Objective:** Map the relationship between wait times, referral departments, and patient satisfaction scores.
* **Visual Reference:** `![Satisfaction Deep-Dive](dashboards/satisfaction_deep-dive.png)`
* **Key Findings:**
  * **The "45-Minute Satisfaction Cliff":** A statistically significant negative correlation exists between wait times and satisfaction. Scores remain stable (averaging 8.2/10) for wait times under 30 minutes, but drop sharply below 5.5/10 when wait times exceed 45 minutes.
  * **Referral Bottlenecks:** Orthopedics and General Practice generate the highest referral volumes. However, Orthopedic referrals experience the longest average wait times, pulling down total departmental satisfaction averages.

---

## Technical Methodology & BI Implementation

### Data Preparation & Cleansing (Python / SQL)
* **DateTime Parsing:** Converted raw date-time strings (`DD-MM-YYYY HH:MM`) into standardized timestamp schemas to enable time-series slicing by year, quarter, month, day of week, and hour.
* **Handling Missing Data:** Addressed null values in `Patient Satisfaction Score` by isolating non-respondents from statistical score averages rather than imputing zero values, preventing artificial skewing of satisfaction KPIs.
* **Data Validation:** Verified data types across boolean flags (`Patient Admission Flag`) and binary indicators (`Patients CM`).

### BI Modeling & DAX Measures (Power BI / Tableau)
* Built a star-schema data model connecting encounter transactions with date and demographic lookup tables.
* Developed custom DAX / Calculated Fields for advanced metrics:
  * `Avg Wait Time = AVERAGE('ER Data'[Patient Waittime])`
  * `Admission Rate % = DIVIDE(CALCULATE(COUNTROWS('ER Data'), 'ER Data'[Patient Admission Flag] = TRUE()), COUNTROWS('ER Data'), 0)`
  * `CSAT Score = CALCULATE(AVERAGE('ER Data'[Patient Satisfaction Score]), NOT(ISBLANK('ER Data'[Patient Satisfaction Score])))`

---

## Strategic Operational Recommendations

1. **Implement Dynamic Shift Scheduling:** Transition from static staffing schedules to dynamic, volume-based staffing models. Reallocate nursing and physician coverage to buffer the 16:00–21:00 arrival surge, directly mitigating wait-time escalation.
2. **Fast-Track Orthopedic & Triage Workflows:** Establish a specialized fast-track triage protocol for musculoskeletal and orthopedic complaints to reduce congestion in the main ER bays and lower wait times for high-volume referral pathways.
3. **Automated Service Recovery Protocols:** Implement an automated threshold alert system in the electronic health record (EHR). When a patient's wait time surpasses 40 minutes, triage supervisors are alerted to initiate clinical reassessment or proactive patient communication, preventing satisfaction drop-offs.
4. **Dedicated Geriatric Case Management Integration:** Embed dedicated case managers within the initial ER triage process for elderly patients (65+) to streamline complex discharge planning and reduce inpatient admission bottlenecks.

---

## Installation & Usage Instructions

### Prerequisites
* [Power BI Desktop](https://powerbi.microsoft.com/) (or equivalent BI viewer) to open visual dashboards.
* [Python 3.8+](https://www.python.org/) with `pandas` and `numpy` installed for running data validation scripts.

### Repository Setup
1. **Clone the project repository:**
   ```bash
   git clone https://github.com/your-username/hospital-er-analysis.git
   cd hospital-er-analysis
   ```
2. **View Dataset:** Access the raw and cleaned datasets in the root directory under `Hospital ER_Data.csv`.
3. **Open Dashboard:** Double-click the Power BI dashboard file (`.pbix`) in your desktop application to explore interactive filters, drill-downs, and underlying DAX formulas.

---
*License: MIT*
