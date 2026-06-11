# 🏭 Production Line Reliability & Maintenance Analysis Dashboard
### Modern Allied Bakeries — Sadat Plant | Engineering Team Analytics Project

> A comprehensive maintenance data analysis project leveraging real-world failure logs from three industrial bakery production lines to compute MTBF, MTTR, and Availability metrics — delivering an actionable, data-driven roadmap for improving Overall Equipment Effectiveness (OEE).

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset & File Breakdown](#-dataset--file-breakdown)
- [Step-by-Step Documentation](#-step-by-step-documentation)
- [Key Findings](#-key-findings)
- [Tools Used](#-tools-used)
- [Team](#-team)

---

## 🔍 Project Overview

**Context:** Modern Allied Bakeries operates three high-volume production lines at the Sadat facility. A persistent capacity problem — where production demand consistently exceeds output — prompted the engineering team to conduct a systematic reliability study.

**Problem Statement (Business Questions Investigated):**
1. What are the current line availability rates?
2. What are the MTBF and MTTR figures for each production line?
3. Which equipment is most critical and requires urgent intervention?
4. What is the improvement action plan for that equipment?
5. What is the approved project plan?

**Objective:** Transform raw daily failure reports spanning multiple months into a structured reliability dashboard that identifies bottlenecks, ranks critical equipment, and supports a data-backed maintenance improvement strategy.

---

## 📁 Dataset & File Breakdown

**File:** `Analysis_Dashboard.xlsx`

The workbook contains **18 sheets** organized across four categories:

### 📊 Business & Summary Sheets
| Sheet | Description |
|---|---|
| `Business Questions` | Defines the 5 core analytical questions driving the project |
| `Summary` | High-level KPIs: Uptime, Failure Count, Downtime, MTBF, MTTR, Availability per line; mechanical vs. electrical failure split |
| `Dashboard` | Visual dashboard (pivot-based; rendered in Excel) |

### 📝 Failure Log Sheets
| Sheet | Description |
|---|---|
| `Failure Recording Log` | Primary dataset — ~1,000+ rows of daily failure events across all lines. Bilingual (Arabic/English). Columns include: Date, Work Order #, Line, Machine Name, Machine Code, Shift, Start/End Time, Duration, Failure Description, Root Cause, Action Taken, Spare Parts, Section (Electrical/Mechanical), Technician, Corrective Y/N, Production Stopped (Y/N), Stoppage Duration, Waste (kg) |
| `Failure Recording Log-D` | Supplementary/daily subset of the same log structure |

### 📈 Analysis Sheets
| Sheet | Description |
|---|---|
| `Line Failure Analysis` | Pivot: Total stoppage time and stoppage count by production line (SA, EU, SC) |
| `Failure Time Analysis` | Pivot: Machine-level stoppage time and count for a specific date/filter |
| `MTBF & MTTR & DT` | Pivot: Per-machine MTBF, MTTR, and downtime for the SA line |
| `Sheet2` | Full EU-line machine-level MTBF, MTTR, and failure count table |
| `Pareto Analysis - EU` | Ranked equipment by stoppage duration and count for the EU line (Pareto logic) |
| `Pareto Analysis - SA` | Ranked equipment by stoppage duration and count for the SA line |

### 🏗️ Equipment Registry Sheets
| Sheet | Description |
|---|---|
| `EU Line` | Full asset list for the European Bread Line — 46 machines with codes, brands, serial numbers, year, model, manufacturer contact, and criticality rating |
| `EU` | Quick-reference machine code lookup for EU assets |
| `SC Line` | Full asset list for the Senn-Crumbs Line — 24 machines |
| `SC` | Quick-reference machine code lookup for SC assets |
| `SA Line` | Full asset list for the Sandwich Line — 32 machines |
| `SA` | Quick-reference machine code lookup for SA assets |
| `VI Line` | Asset registry for the Vienna Line (additional line, 12 machines) |
| `UT List` / `UT` | Utilities equipment list (boilers, compressors, refrigeration, generators) |
| `CH Processing` | Chocolate processing equipment registry |
| `Team` | List of ~40 maintenance technicians by name |

---

## 🛠️ Step-by-Step Documentation

### Step 1 — Data Collection
Raw failure events were recorded by maintenance technicians across every shift (First / Second / Third) in the `Failure Recording Log` sheet. Each row captures a single failure event, with start and end timestamps stored as Excel serial fractions (converted to hours). Bilingual field headers (Arabic + English) ensure on-floor usability.

### Step 2 — Data Cleaning & Standardization
- Machine codes (e.g., `SA-AIJ-001`, `EU-PRF-002`) were standardized across all sheets.
- Failure duration values were computed from raw timestamp fractions (`To - From`).
- Production stoppage flags (`Yes/No`) and waste quantities (kg) were captured for each event.
- Root cause and action fields were filled by the attending technician in Arabic.

### Step 3 — KPI Computation
Three core reliability metrics were calculated per line and per machine:

| Metric | Formula |
|---|---|
| **MTBF** (Mean Time Between Failures) | `Total Operating Hours / Number of Failures` |
| **MTTR** (Mean Time To Repair) | `Total Downtime Hours / Number of Failures` |
| **Availability** | `Uptime / (Uptime + Downtime)` |

These were aggregated in the `Summary` sheet and detailed machine-level breakdowns in `Sheet2` and the `MTBF & MTTR & DT` sheet.

### Step 4 — Failure Cause Classification
All failures were categorized into two root-cause buckets:
- **Mechanical** — physical wear, breakage, misalignment, jamming
- **Electrical** — sensor faults, motor trips, inverter failures, wiring issues

The `Summary` sheet computes the mechanical/electrical split per line by summing downtime hours for each category.

### Step 5 — Line-Level & Machine-Level Analysis
Pivot tables in `Line Failure Analysis` and `Failure Time Analysis` aggregate:
- Total stoppage time and count per line
- Per-machine ranking by stoppage duration and frequency

### Step 6 — Pareto (80/20) Analysis
The `Pareto Analysis - EU` and `Pareto Analysis - SA` sheets rank all machines by both cumulative stoppage duration and cumulative failure count, enabling the team to identify which 20% of machines cause 80% of downtime.

### Step 7 — Dashboard Visualization
The `Dashboard` sheet (Excel-rendered) consolidates all KPIs into a visual overview for management review — answering the five business questions defined at project inception.

---

## 📊 Key Findings

### 🔢 Line Availability (As-Is)
| Production Line | Uptime (Days) | Failures | Downtime (Days) | MTBF (Days) | MTTR (Days) | **Availability** |
|---|---|---|---|---|---|---|
| **SC** (Senn-Crumbs) | 84.37 | 131 | 5.63 | 0.644 | 0.043 | **93.74%** |
| **EU** (European Bread) | 75.93 | 414 | 14.07 | 0.183 | 0.034 | **84.36%** |
| **SA** (Sandwich) | 72.76 | 449 | 17.24 | 0.162 | 0.038 | **80.84%** |

> **SC Line** is the most reliable. **SA Line** is the most critical bottleneck with the lowest availability, highest failure count, and most downtime.

---

### ⚙️ Failure Cause Split

| Line | Mechanical Failures (% of DT) | Electrical Failures (% of DT) |
|---|---|---|
| EU | 65.9% | 34.1% |
| SA | 73.1% | 25.2% |
| SC | 63.2% | 36.8% |

> Mechanical failures dominate across all three lines. SA's mechanical share is the highest at 73%, pointing to aging mechanical components as the primary reliability driver.

---

### 🔴 Most Critical Equipment (Top Offenders by Downtime)

**SA Line — Top 5 by Stoppage Duration:**
1. 🥇 **Automatic Injection Machine (COMAS)** `SA-AIJ-001` — 3.78 hrs downtime | 62 failures | MTBF: 0.48 days
2. 🥈 **OLD AMF Divider** `SA-DVD-001` — 1.08 hrs | 27 failures
3. 🥉 **Date Coding Machine (1)** `SA-DCD-001` — 0.93 hrs | 23 failures
4. **Packaging Machine (1)** `SA-PAC-001` — 0.57 hrs | 18 failures
5. **Mixer (1)** `SA-MIX-001` — 0.56 hrs | 18 failures

**EU Line — Top 5 by Stoppage Duration:**
1. 🥇 **Rounder (AMF)** `EU-RON-001` — 0.33 hrs | 1 failure (long MTTR)
2. 🥈 **Date Coding Machine (1)** `EU-DCD-001` — 0.15 hrs | 2 failures
3. 🥉 **LeMatich Packing Machine** `EU-PCM-003` — 0.08 hrs | 3 failures
4. **Proofer** `EU-PRF-002` — 0.075 hrs | 6 failures
5. **Pan Conveyor (1)** `EU-PAC-001` — 0.038 hrs | 3 failures

---

### 💡 Improvement Action Plan Insights

Based on the Pareto analysis and MTBF/MTTR data, the recommended priority interventions are:

- **SA-AIJ-001 (COMAS Injection Machine):** Highest combined impact. Recurring base breakage, needle failures, and sensor faults indicate need for a full scheduled overhaul, replacement of wear parts (bases, needles, chains), and operator training. MTBF of only ~0.48 days is unsustainable.
- **SA-DVD-001 (OLD AMF Divider):** Persistent weight calibration failures and screw/paddle wear. A planned replacement or full mechanical refurbishment should be scheduled.
- **EU-PCM-003 (LeMatich Packing Machine):** Repeated sealing heater, knife, and mid-seal issues. Preventive heater replacement schedule recommended.
- **SC-DRY-001 (Bread Dryer):** Frequent belt failures and conveyor issues. Belt replacement cycle should be shortened based on observed wear rate.
- **SC-OVN-001 (SC Baking Oven):** High frequency of belt misalignment and igniter faults. Alignment jigs and routine burner checks recommended.

---

### 📉 Waste Impact
Production stoppage events were linked to waste quantities (kg). Several single failures generated 250–1,325 kg of product waste, underscoring the direct cost of unplanned downtime beyond lost production hours.

---

## 🧰 Tools Used

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Primary platform — pivot tables, KPI computation, Pareto charts, dashboard |
| **Arabic + English bilingual data entry** | On-floor failure recording by maintenance technicians |
| **MTBF / MTTR / Availability formulas** | Reliability engineering calculations (ISO 14224 aligned) |
| **Pareto Analysis** | 80/20 prioritization of critical equipment |
| **Pivot Tables & Charts** | Line-level and machine-level aggregation and visualization |

---

## 👥 Team

**Engineering Maintenance Team — Modern Allied Bakeries, Sadat Plant**

The project involved ~40 maintenance technicians across electrical and mechanical disciplines, recording and analyzing failures across three shifts per day. Data spans the full production calendar period captured in the failure log (January 2023 onward).

---

## 📌 How to Use This Repository

1. Open `Analysis_Dashboard.xlsx` in Microsoft Excel (2016 or later recommended).
2. Navigate to the **Dashboard** sheet for the executive summary view.
3. Use the **Summary** sheet for line-level KPI comparison.
4. Drill into **Pareto Analysis - SA** and **Pareto Analysis - EU** to identify priority machines.
5. Filter the **Failure Recording Log** by machine code or date range for root cause deep-dives.
6. Reference **EU Line**, **SC Line**, and **SA Line** sheets for manufacturer contact details when ordering spare parts.

---

> *This project is part of the Modern Allied Bakeries Engineering Team's continuous improvement initiative aimed at achieving ≥95% availability across all production lines.*
