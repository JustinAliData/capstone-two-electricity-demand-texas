# Texas Electricity Demand Forecasting

> Forecasting hourly electricity demand in ERCOT regions to support grid balancing and capacity planning.

**Stack:** Python · Pandas · NumPy · scikit-learn · Matplotlib
**Status:** In progress — Springboard Capstone Two
**Author:** Justin Ali · [LinkedIn](https://www.linkedin.com/in/justin-ali-data/)

---

## The problem

Texas's ERCOT grid is uniquely exposed: it's largely isolated from the U.S. interconnections, summer demand peaks are extreme, and the 2021 winter storm made the cost of bad forecasts painfully clear. Even modest improvements in short-horizon demand forecasts translate directly into lower grid-balancing costs and reduced risk of load shedding. This project builds a forecasting pipeline for hourly demand in Texas regions, framed as a model that an operations team could iterate on.

## The data

- **Source:** [Hourly Electricity Demand and Production (U.S.)](https://www.kaggle.com/datasets/paolodelia/hourly-electricity-demand-and-production-us) on Kaggle
- **Coverage:** Hourly electricity demand and production across U.S. balancing authorities; this project filters to ERCOT / Texas regions
- **Notable quirks:** Mixed timezones across regions, gaps in early-period data, occasional negative values from reporting corrections

## Approach

1. **EDA & cleaning** — Standardize timezones to UTC, profile gaps and outliers, characterize daily/weekly/annual seasonality.
2. **Feature engineering** — Calendar features (hour, day-of-week, month, holiday), lagged demand (1h, 24h, 168h), rolling means and standard deviations.
3. **Modeling** — Start with a seasonal-naive baseline, then tree-based regressors (LightGBM / Random Forest) on the engineered features.
4. **Validation** — Time-series cross-validation with an expanding window. Primary metrics: MAE and MAPE (interpretable to operations); secondary: RMSE.
5. **Tuning** — Hyperparameter search on the best-performing model family.

## Results

*(In progress — table and chart will be added as modeling completes.)*

| Model | MAE (MW) | MAPE | Notes |
|---|---|---|---|
| Seasonal naive (t − 168h) | _TBD_ | _TBD_ | baseline |
| LightGBM (tuned) | _TBD_ | _TBD_ | final |

## What I'd do next

- Incorporate weather features (temperature, dew point) from NOAA — the single biggest known driver of demand in Texas.
- Build a hierarchical model that forecasts ERCOT sub-regions and reconciles to the system total.
- Add prediction intervals via quantile regression, not just point forecasts — operations cares about the upper tail.
- Wrap the final model in a small FastAPI service that returns next-24-hour forecasts on demand.

## Repo contents

```
.
├── Capstone_Two_Project_Proposal_Justin_Ali.pdf   # written proposal
├── notebooks/                                     # to be added
└── README.md
```

## How to run

```bash
git clone https://github.com/JustinAliData/capstone-two-electricity-demand-texas.git
cd capstone-two-electricity-demand-texas
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

## Acknowledgments

Built as part of the **Springboard Data Science Career Track** (Capstone Two).
