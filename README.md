# 🏨 Hotel Booking Demand — Resort Hotel Analytics & Cancellation Insights

> Professional, employer‑ready project README for your Kaggle "Hotel Booking Demand" (Resort Hotel only) case study.

---

## Overview

This project analyzes **booking behavior, seasonality, pricing (ADR), and cancellation drivers** for a **Resort Hotel in Portugal** using the public *Hotel Booking Demand* dataset (119,390 bookings; **2015‑07 → 2017‑08**). The goal is to support:

* **Revenue management** (peak seasons, ADR trends, revenue drivers)
* **Cancellation mitigation** (factors, early warning, policy levers)
* **Channel strategy** (OTA vs Direct vs Corporate)
* **Guest segmentation** (families, couples, repeat guests)

> Scope: Resort Hotel only (leisure‑driven, highly seasonal) for clearer strategy signals.

---

## Highlights

* 📊 **Power BI dashboard**: Executive KPIs, Cancellation Insights, Guest & Channel views
* 🧪 **Logistic Regression**: Predicts cancellation probability from lead_time, deposit_type, channel, ADR, guest history
* 🧱 **Clean repo structure** with notebooks, data, Power BI, and docs
* 🧭 **Business recommendations** aligned to revenue & operations

---

## Table of Contents

* [Overview](#overview)
* [Highlights](#highlights)
* [Dataset](#dataset)
* [Key Features (Fields)](#key-features-fields)
* [Feature Engineering](#feature-engineering)
* [Analysis Plan](#analysis-plan)
* [Power BI Dashboard](#power-bi-dashboard)
* [Modeling (Logistic Regression)](#modeling-logistic-regression)
* [Results & Insights](#results--insights)
* [Project Structure](#project-structure)
* [Quickstart](#quickstart)
* [DAX Measures (snippet)](#dax-measures-snippet)
* [Interview Talking Points](#interview-talking-points)
* [License](#license)

---

## Dataset

* Source: Kaggle — *Hotel Booking Demand* (Resort + City hotels, Portugal)
* Period: **2015‑07 to 2017‑08**
* Observations: **119,390** bookings (both completed & canceled)
* This project filters to **Resort Hotel** only.

> Alternative supporting datasets (optional for future work): City‑hotel revenue monthly series, STR‑style RevPAR dataset.

---

## Key Features (Fields)

**Stay & Party**: `stays_in_weekend_nights`, `stays_in_week_nights`, `adults`, `children`, `babies`

**Channel & Market**: `market_segment`, `distribution_channel`, `meal`, `country`

**Behavior & History**: `is_repeated_guest`, `previous_cancellations`, `previous_bookings_not_canceled`, `booking_changes`, `days_in_waiting_list`

**Pricing & Deposits**: `adr`, `deposit_type` (No Deposit / Non Refund / Refundable)

**Outcome**: `is_canceled`, `reservation_status`, `reservation_status_date`

---

## Feature Engineering

* `stay_length = stays_in_weekend_nights + stays_in_week_nights`
* `revenue = adr * stay_length`
* `arrival_month` (ordered month for seasonality)
* `loyalty_ratio = previous_bookings_not_canceled / (previous_bookings_not_canceled + previous_cancellations + 1)`
* Encodings for categorical variables (for ML): `deposit_type`, `market_segment`, `distribution_channel`, `customer_type`, `meal`

---

## Analysis Plan

**EDA (Python)**

* Data cleaning, nulls, outliers (ADR), category normalization
* Seasonality: bookings & ADR by month; lead_time distributions
* Channel performance: OTA vs Direct vs Corporate; cancellation rates
* Segmentation: repeat vs new; family vs couple; stay_length patterns

**KPIs**

* Bookings, ADR, Revenue, Cancellation Rate, Repeat Guest %, Avg. Lead Time

---

## Power BI Dashboard

**Pages**

1. **Executive KPI** — Bookings/Revenue trend, ADR, Cancellation Rate, slicers (Hotel Type, Year/Month, Channel)
2. **Cancellation Insights** — Lead Time vs Cancellation, Deposit Type impact, Channel comparison
3. **Guest & Channel** — Country map, Party composition, Repeat guest ratio, Stay length vs ADR

**Screenshots**

> Add exported images here:

* `/powerbi/screenshots/overview.png`
* `/powerbi/screenshots/cancellation.png`
* `/powerbi/screenshots/segments.png`

---

## Modeling (Logistic Regression)

**Target**: `is_canceled` (1/0)

**Candidate features**: `lead_time`, `deposit_type`, `distribution_channel`, `market_segment`, `adr`, `previous_cancellations`, `previous_bookings_not_canceled`, `booking_changes`, `stay_length`, `customer_type`

**Metrics**

* Accuracy, Precision, **Recall** (prioritize catching true cancellations), ROC‑AUC

**Artifacts**

* Notebook: `/notebooks/model.ipynb`
* Model plot: feature importance bar chart

---

## Results & Insights

> Replace placeholders with your findings.

* **Seasonality**: Peak demand in *Jul–Aug* with elevated ADR (x%)
* **Cancellations**: Overall rate ~ *x%*; driven by **long lead_time** and **OTA channels**
* **Deposits**: *Non‑refundable* vs *No deposit* shows **Δ cancellation rate = x pp**
* **Guests**: Repeat guests cancel less (−x pp) and yield **higher revenue reliability**
* **Actions**: Shorten free‑cancellation window for long lead times; incentivize **Direct** bookings; dynamic deposit policy by season

---

## Project Structure

```
Hotel-Booking-Analytics/
├─ data/
│  ├─ raw/
│  └─ processed/
├─ notebooks/
│  ├─ EDA.ipynb
│  └─ model.ipynb
├─ powerbi/
│  ├─ hotel_dashboard.pbix
│  └─ screenshots/
├─ models/
│  └─ (optional saved model)
├─ docs/
│  ├─ insights.pdf
│  └─ interview_script.md
└─ README.md
```

---

## Quickstart

**1) Clone & environment**

```bash
git clone https://github.com/<your-username>/Hotel-Booking-Analytics.git
cd Hotel-Booking-Analytics
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt
```

**2) Data**

* Place original CSV in `/data/raw/`
* Notebooks save processed files into `/data/processed/`

**3) Run notebooks**

```bash
jupyter lab  # open EDA.ipynb and model.ipynb
```

**4) Power BI**

* Open `/powerbi/hotel_dashboard.pbix`
* Point to `/data/processed/` if prompted

---

## DAX Measures (snippet)

```DAX
Revenue := SUMX( 'Bookings', 'Bookings'[adr] * 'Bookings'[stay_length] )

Bookings := COUNTROWS( 'Bookings' )

ADR := DIVIDE( [Revenue], SUM( 'Bookings'[stay_length] ) )

Cancellation Rate := AVERAGE( 'Bookings'[is_canceled] )

Repeat Guest % := DIVIDE(
  CALCULATE( COUNTROWS('Bookings'), 'Bookings'[is_repeated_guest] = 1 ),
  [Bookings]
)

Avg Lead Time := AVERAGE( 'Bookings'[lead_time] )
```

> Adjust table/column names to your model (e.g., `Bookings` vs `FactBookings`).

---

## Interview Talking Points

* Framed the work as a **revenue management** problem (not just EDA)
* Built **BI views** for executives and **risk views** for operations
* Prioritized **Recall** to minimize surprise cancellations
* Translated signals (lead_time, deposit, channel) into **policy levers** (cxl window, deposit rules, direct‑booking incentives)

---

## License

MIT (or your preferred license). Add `LICENSE` file in repo root.

---

### Notes (CN)

* 本项目聚焦度假酒店（Resort），强调季节性与休闲客群，对 **价格策略 / 取消率 / 渠道** 给出可执行建议。
* README 为作品集版式：先业务目标，再技术细节，最后方法论与结论，方便招聘方快速理解价值。
