# 🌞 Solar Energy Forecasting — Saudi Arabia

A comprehensive time series forecasting project that predicts **Global Horizontal Irradiance (GHI)** across Saudi Arabia using statistical, machine learning, and deep learning models.

---

## 📌 Project Overview

Saudi Arabia receives some of the highest solar irradiance in the world, making accurate solar energy forecasting critical for grid management and renewable energy planning. This project builds and compares **13 forecasting models** across three model families to identify the most accurate approach for monthly GHI prediction.

**Dataset:** Monthly solar and weather measurements sourced across **42 industrial and major cities** spanning all Saudi regions (2017–2021), aggregated into a comprehensive national average time series of 60 data points.
**Data Source:** Officially sourced from the **Saudi National Open Data Platform** (منصة البيانات المفتوحة السعودية).

---

## 🗂️ Project Structure

```text
├── Time_Series_project.ipynb   # Main notebook
└── README.md
```
---

## 🔄 Workflow

1. **Time Series Exploration** — Visualizing trends, distributions, and seasonality
2. **Stationarity Testing** — ADF test on the original and differenced series
3. **Time Series Decomposition** — Separating trend, seasonality, and residuals
4. **Missing Date Imputation** — Linear interpolation across a complete 60-month range
5. **Feature Engineering** — Lag features (up to 12 months), rolling mean/std windows
6. **Train / Test Split** — Temporal split (no random shuffling) to simulate real forecasting
7. **Model Building** — 9 models across 3 families
8. **Comparison & Selection** — Ranked by RMSE and MAE

---

## 🤖 Models Used

### Statistical
| Model | Description |
|-------|-------------|
| ARMA | Applied on first-differenced series |
| ARIMA | Handles non-seasonal trends |
| SARIMA | Handles both trend and seasonality |

### Machine Learning
| Model | Key Hyperparameters |
|-------|---------------------|
| Linear Regression | Baseline ML model |
| Decision Tree | `max_depth=5` |
| Random Forest | `n_estimators=300`, `max_depth=8` |
| Gradient Boosting | `n_estimators=300`, `learning_rate=0.05` |
| XGBoost | `n_estimators=300`, `subsample=0.8` |

### Deep Learning
| Model | Architecture |
|-------|-------------|
| Simple RNN | 50 units, Dropout 0.2 |
| LSTM | 64 units, Dropout 0.2 |
| GRU | 64 units, Dropout 0.2 |

All deep learning models use:
- Input window: 12 months
- Optimizer: Adam
- Loss: MSE
- Early stopping: patience=10

---

## 📊 Evaluation Metrics

- **RMSE** (Root Mean Squared Error) — primary selection criterion
- **MAE** (Mean Absolute Error)
- **AIC** — for statistical model selection only
---

### 🏆 Model Performance Summary

Below is the comprehensive performance ranking of all 11 developed models, sorted from the lowest error (best) to the highest error:

| Rank | Model | Model Family | Test RMSE | Test MAE | Status |
| :---: | :--- | :--- | :---: | :---: | :--- |
| **1** | **Linear Regression** | Machine Learning | **157.44** | **119.16** | 🏆 **Best Performer (Winner)** |
| **2** | **XGBoost** | Machine Learning | **267.85** | **215.13** | Strong ML Baseline |
| **3** | **Random Forest** | Machine Learning | **304.08** | **236.00** | — |
| **4** | **Simple RNN** | Deep Learning | **312.93** | **261.69** | Best Deep Learning |
| **5** | **ARIMA** | Statistical | **359.25** | **307.20** | — |
| **6** | **SARIMA** | Statistical | **395.41** | **339.35** | — |
| **7** | **Gradient Boosting** | Machine Learning | **415.64** | **292.68** | — |
| **8** | **ARMA** | Statistical | **496.17** | **423.84** | — |
| **9** | **Baseline** | Statistical | **535.28** | **436.89** | — |
| **10** | **Decision Tree** | Machine Learning | **541.03** | **414.93** | — |
| **11** | **Baseline_ML** | Machine Learning | **582.42** | **495.33** | — |
| **12** | **LSTM** | Deep Learning | **1619.12** | **1475.56** | Overfitted due to data size |
| **13** | **GRU** | Deep Learning | **1700.13** | **1519.14** | Overfitted due to data size |

> 📌 **Key Insight & Conclusion:** > The **Linear Regression** model significantly outperformed all other configurations, achieving the lowest error rates ($RMSE = 157.44$, $MAE = 119.16$). 
>
> In time series forecasting with small datasets (60 data points), simpler models often generalize much better than complex architectures. Complex deep learning models like **LSTM** and **GRU** suffered from severe overfitting because they require a massive volume of historical data to properly optimize their dense weight matrices, which explains their high error rates compared to the robust, lower-variance Linear Regression baseline.

---

### 📈 Visualizing Model Performance

Below is a bar chart comparing the Root Mean Squared Error (RMSE) across all evaluated statistical, machine learning, and deep learning models. Lower values indicate better forecasting accuracy:

<img width="1085" height="624" alt="download (2)" src="https://github.com/user-attachments/assets/e9d38cb1-5efb-4d56-accb-8b8768e7b79c" />

## 🚀 Getting Started

This notebook was developed in **Google Colab**. To run it:

1. Upload `full_solar_dataset.csv` to your Google Drive or Colab session
2. Update the dataset path in the first code cell:
   ```python
   df = pd.read_csv('/content/full_solar_dataset.csv')
   ```
3. Run all cells in order

### Requirements

```
pandas
numpy
matplotlib
scikit-learn
statsmodels
xgboost
tensorflow
```

Install via:
```bash
pip install pandas numpy matplotlib scikit-learn statsmodels xgboost tensorflow
```

---

## 👥 Author

* **Talal Alshehri**
  * *Role:* End-to-end Machine Learning & Deep Learning Development, Feature Engineering, Time Series Modeling (13 Models), and Evaluation.

---
*Developed as part of the **Time Series Analysis using Python** program at **Tuwaiq Academy**.* 🚀
