# British Airways – Data Science Tasks

This repository contains two data science projects for British Airways: **Part 1** (Lounge Eligibility Lookup for Terminal 3 planning) and **Part 2** (Customer Booking Prediction for proactive acquisition).

---

## Part 1: Lounge Eligibility Lookup Table

### Description

Builds a **reusable lookup table** that estimates lounge eligibility percentages (Tier 1, Tier 2, Tier 3) by flight category. Designed for BA’s Terminal 3 planning and can be applied to future schedules without needing exact flight or aircraft details.

### Data

| File | Description |
|------|-------------|
| `British Airways Summer Schedule Dataset - Forage Data Science Task 1.xlsx` | BA summer flight schedule (10,000 rows) with columns: FLIGHT_DATE, FLIGHT_TIME, TIME_OF_DAY, FLIGHT_NO, DEPARTURE_STATION_CD, ARRIVAL_STATION_CD, ARRIVAL_REGION, HAUL, AIRCRAFT_TYPE, seat counts, TIER1/2/3_ELIGIBLE_PAX |
| `lookup.xlsx` | Output lookup table: lounge eligibility % by route type and time of day |

### Code

| File | Description |
|------|-------------|
| `trial.ipynb` | Loads the schedule, groups flights by **route type** (Short-haul, Mid-haul A, Mid-haul B, Long-haul, Unknown) and **time of day** (AM/PM), computes or assigns Tier 1/2/3 % per grouping, and produces the reusable lookup table |

### Logic

- **Route type** from HAUL + ARRIVAL_REGION: Short-haul (Europe), Mid-haul A (Europe/Middle East long-haul), Mid-haul B (North America), Long-haul (Asia/Africa), Unknown
- **Time of day** from TIME_OF_DAY: Morning/Lunchtime → AM, Afternoon/Evening → PM
- Each flight gets one **Grouping** (e.g. "Short-haul PM"); the lookup returns Tier 1 %, Tier 2 %, Tier 3 % and Notes
- **Lounge tiers:** Tier 1 (Concorde Room), Tier 2 (First Lounge), Tier 3 (Club Lounge)

### Output

A lookup table mapping each grouping to estimated lounge eligibility percentages, usable for future schedules to estimate lounge demand.

---

## Part 2: Customer Booking Prediction

### Description

Predictive model to identify customers likely to **complete a booking** (`booking_complete`). Built for proactive customer acquisition—airlines must be proactive to acquire customers before they embark on their holiday.

### Data

| File | Description |
|------|-------------|
| `customer_booking.csv` | Customer booking data (50,000 rows). Columns: num_passengers, sales_channel, trip_type, purchase_lead, length_of_stay, flight_hour, flight_day, route, booking_origin, wants_extra_baggage, wants_preferred_seat, wants_in_flight_meals, flight_duration, **booking_complete** (target) |

### Code

| File | Description |
|------|-------------|
| `Getting Started.ipynb` | EDA, feature engineering, categorical encoding, Random Forest classifier, cross-validation, feature importance plot, and one-slide executive summary (PowerPoint) |

### Logic

1. **EDA:** Target balance (~15% complete), categorical value counts, numeric distributions, correlation heatmap
2. **Preparation:** Optional features (weekend, purchase_lead_bin, add_ons_count), grouped high-cardinality categoricals (route, booking_origin), OneHotEncoder for categoricals, stratified 80/20 train/test split
3. **Model:** Random Forest with `class_weight="balanced"` for imbalance
4. **Evaluation:** 5-fold CV (accuracy, precision, recall, F1, ROC-AUC), test-set metrics, confusion matrix, feature importance bar chart
5. **Reporting:** Generates `Booking_Prediction_Summary.pptx` with results and top drivers

### Output

- Model metrics (accuracy, F1, ROC-AUC, etc.)
- Feature importance plot (how each variable contributes to predictions)
- `Booking_Prediction_Summary.pptx` (one-slide summary for managers)

---

## Project Structure

```
british-airways/
├── Part 1
│   ├── British Airways Summer Schedule Dataset - Forage Data Science Task 1.xlsx
│   ├── lookup.xlsx
│   └── trial.ipynb
├── Part 2
│   ├── customer_booking.csv
│   └── Getting Started.ipynb
├── requirements.txt
└── README.md
```

## Setup

```bash
# Clone the repo
git clone <your-repo-url>
cd british-airways

# Create virtual environment (optional)
python -m venv venv
venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt
```

## Usage

**Part 1:** Open `trial.ipynb` and run all cells to build the lounge eligibility lookup table.

**Part 2:** Open `Getting Started.ipynb` and run all cells. The last cell generates `Booking_Prediction_Summary.pptx` (requires `python-pptx`).

## Dependencies

- pandas
- scikit-learn
- matplotlib
- seaborn
- python-pptx
- openpyxl (for reading xlsx files)
