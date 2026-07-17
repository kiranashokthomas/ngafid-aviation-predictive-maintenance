# NGAFID Aviation Predictive Maintenance

![Python](https://img.shields.io/badge/Python-3.10-blue) ![Status](https://img.shields.io/badge/Status-Baseline%20Complete-brightgreen) ![License](https://img.shields.io/badge/License-MIT-green)

End-to-end predictive maintenance project using the **National General Aviation Flight Information Database (NGAFID)** — the largest publicly available annotated fleet-wide dataset for aviation maintenance research. This project predicts whether a flight occurs **within 2 days before an unplanned maintenance event**, enabling proactive fault detection and reducing unscheduled aircraft downtime.

---

## Dataset

- **Source:** [NGAFID Aviation Maintenance Dataset — Kaggle](https://www.kaggle.com/datasets/hooong/aviation-maintenance-dataset-from-the-ngafid)
- **Size:** 31,177 hours of real general aviation flight data across 28,935 flights
- **Maintenance events:** 2,111 unplanned maintenance events across 36 fault types
- **Structure:** `flight_header.csv` (flight-level index) and `flight_data.pkl` (23 sensor channels per flight)

> The full dataset must be downloaded from Kaggle. A sample label file (`flight_header.csv`) is included in this repo for reference.

---

## Project Goals

- Build flight-level features from raw multivariate sensor time-series
- Define a binary classification target: maintenance within 2 days (pre-event) vs. all other flights
- Train and evaluate baseline ML models (Random Forest / XGBoost)
- Export results for Power BI dashboard visualisation
- Compare against published benchmark models

---

## Methodology

1. **Feature Engineering** — Summarise each flight's raw sensor array (timesteps x 23 channels) into statistical features (mean, std, min, max per channel), producing 92 features per flight
2. **Target Definition** — Positive (1) = flights within 2 days before a maintenance event; Negative (0) = all others
3. **Class Imbalance** — Handled using `class_weight='balanced'` in RandomForestClassifier
4. **Evaluation** — ROC-AUC, Precision, Recall, F1-Score, Confusion Matrix

---

## Results (Baseline)

| Metric | Score |
|---|---|
| Model | Random Forest (balanced) |
| Features | 92 statistical features (23 channels x 4 stats) |
| Target | Binary: maintenance within 2 days |
| Evaluation | ROC-AUC, Precision, Recall, F1 |
| Status | Baseline pipeline complete — model tuning ongoing |

> This is a portfolio baseline. The pipeline is complete end-to-end. Model performance metrics will be added after hyperparameter tuning.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python, Google Colab | Development environment |
| Pandas, NumPy | Data handling and feature engineering |
| Scikit-learn, XGBoost | Machine learning models |
| Power BI | Dashboard visualisation |
| GitHub | Version control |

---

## Business Impact

Shifts aircraft maintenance from reactive to proactive, reducing unscheduled AOG (Aircraft on Ground) events. Gives MRO teams a 2-day lead time to source parts and plan resources before a fault grounds an aircraft.

---

## Author

**Kiran Ashok Thomas**
MSc Aviation Digital Technology & Management — Cranfield University (Distinction)
GitHub: [kiranashokthomas](https://github.com/kiranashokthomas)
