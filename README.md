# SafeBoda Day & Time Pricing Analysis

Investigating whether — controlling for distance and duration — the day of the week and time of day affect SafeBoda ride-hailing peak-hour surcharges, and uncovering the pattern behind that pricing.

## 1. Problem Statement

- **Question:** Does SafeBoda charge different peak-hour surcharges for otherwise similar trips depending on the day of the week and the time of day?
- **Who cares:** Frequent SafeBoda riders who want to minimise transport costs, and analysts interested in dynamic pricing patterns for ride-hailing services in East Africa.

## 2. Data

- **Source:** Personal SafeBoda trip receipts (Uganda).
- **Time period / geography / units:** March – April 2026; Kampala, Uganda; prices in Ugandan Shillings (UGX); distance in km; duration in minutes.
- **Main file:** `safeboda_trips.csv` — 50 trips with 22 variables including `date`, `time`, `distance_km`, `duration_min`, `peak_hour_price_ugx`, `price_per_km_ugx`, `price_per_minute_ugx`, `base_fare_ugx`, and `order_total_ugx`.
- **Key cleaning / transformations:**
  - Extracted `day` (day-of-week name) and `hour` from raw `date` and `time` columns.
  - Bucketed `hour` into five `time_of_day` categories: Early morning (0–6), Late morning (6–9), Early afternoon (9–12), Late afternoon (12–18), Evening (18–24).

## 3. Methodology

- **Tools and libraries:** Python, pandas, seaborn, matplotlib.
- **Main steps:**
  1. **EDA** – univariate distribution of `peak_hour_price_ugx` (histogram + boxplot).
  2. **Feature engineering** – created `day` and `time_of_day` categorical features.
  3. **Aggregation** – computed median peak-hour price grouped by day, by time-of-day, and by the combined day × time-of-day cross-tabulation.
  4. **Visualization** – boxplots per group and a heatmap of the day × time-of-day pivot table.
- **Important definitions:**
  - `peak_hour_price_ugx` – the surge component of the fare, isolated from base fare, per-km, and per-minute charges; used as the primary metric throughout.

## 4. Results and Insights

- **Time of day dominates pricing:** Evening trips (18:00–24:00) carry the highest surcharges across almost every day (~1 500–1 571 UGX), while late-morning trips (9:00–12:00) are consistently cheapest (~668–724 UGX). Riders can save significantly by scheduling non-urgent trips in the late morning.
- **Monday evening is the single most expensive slot:** Median peak surcharge of ~1 536 UGX — countering the initial hypothesis that Wednesday evening would top the rankings. Thursday and Wednesday late-afternoon slots follow closely.
- **Day of week is a secondary effect:** Wednesday has the highest overall median (1 488 UGX) and Sunday the lowest (1 059.5 UGX), but the within-day time-of-day variation is larger than the between-day variation.
- **Notebook / report:** [`notebook.ipynb`](notebook.ipynb)

## 5. Repository Structure

- `safeboda_trips.csv` – raw trip data collected from personal SafeBoda receipts
- `notebook.ipynb` – end-to-end EDA and visualisation notebook

## 7. How to Run

```bash
# clone repo
git clone https://github.com/delightaheebwa/safeboda-dt-analysis.git
cd safeboda-dt-analysis

# create environment and install deps
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install pandas seaborn matplotlib jupyter

# run analysis
jupyter notebook notebook.ipynb
```
