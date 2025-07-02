#  Alternative Data Alpha Mining using Reddit, News & Google Trends with ML Backtesting

This project explores **alpha generation** using **alternative data sources**—Reddit sentiment, financial news, and Google Trends—to **predict stock returns**. We apply **Random Forest** and **LightGBM** models, introduce **confidence thresholding**, and conduct **rolling-window backtesting** to assess strategy robustness.

---

##  Table of Contents

- [1. Project Structure](#-project-structure)
- [2. Approach](#-approach)
- [3. Datasets](#️-datasets)
- [4. Features](#️-features)
- [5. Modeling](#-modeling)
- [6. Backtesting](#-backtesting)
- [7. Outputs](#-outputs)
- [8. Results](#-results)
- [9. Installation](#-installation)
- [10. Running the Code](#-running-the-code)
- [11. Dependencies](#-dependencies)
- [12. Acknowledgements](#-acknowledgements)
- [13 Author](#-author)

---

##1.  Project Structure

DataAlpha/
├── data/
│ ├── raw/
│ │ ├── News_Headline/
│ │ ├── social_media/
│ │ └── returns/
│ └── processed/
│ └── final_merged_scores_with_features.csv
├── notebooks/
│ └── EDA_and_Modeling.ipynb
├── outputs/
│ └── plots/
├── src/
│ ├── feature_engineering.py
│ ├── model_training.py
│ └── backtesting.py
├── .gitignore
├── requirements.txt
└── README.md


---

## 2. Approach

We predict **daily stock direction (up/down)** using:

- 🧵 **Reddit** sentiment (e.g., WallStreetBets)
- 📰 **News** sentiment (e.g., ABC News)
- 📈 **Google Trends** search interest

We extract, merge, and transform this alternative data to train models that make **confident predictions**, validated through **rolling-window backtesting**.

---

## 3. Datasets

| Source                       | Type             | Description                     |
| ---------------------------- | ---------------- | ------------------------------- |
| `r_wallstreetbets_posts.csv` | Reddit Sentiment | Daily aggregated WSB sentiment  |
| `abcnews-date-text.csv`      | News Headlines   | ABC news title sentiment        |
| `google_trends.csv`          | Google Trends    | Daily search score for tickers  |
| `returns/`                   | Price Data       | Daily returns (e.g., AAPL, WMT) |

>  Some files are large and tracked via **Git LFS**.

---

## 4. Features

We engineered:

- **Return-based features**: `return`, `return_lag1`, `return_roll3`, `return_delta`
- **Sentiment features**: `reddit_sentiment`, `news_sentiment`, `trend_score`
- **Lag & rolling features**: 3-day, 7-day rolling stats
- **Momentum & agreement**:
  - `trend_momentum`: trend3 - trend7
  - `signal_agreement`: agreement between signals
- **Interaction terms**: `reddit_trend_agree`, `news_trend_agree`
- **Volatility**: `return_volatility_5`
- **Target**: Binary label `target_up` (next-day return > 0)

---

## 5. Modeling

We experimented with:

- **Random Forest** (The best model)
- **LightGBM**

 Key Strategies:

- **Imbalance handling**: `class_weight='balanced'`
- **Feature selection**: Top 15 from RF importance
- **Confident prediction only**:
  - Predict if `P(class) > 0.65` or `< 0.35`

---

## 6. Backtesting

A **rolling-window backtest** setup:

-  **60-day training** →  **20-day testing**
- Sliding forward one window at a time
- Only **confident predictions** used for evaluation

 Metrics Tracked:

- Accuracy
- Cumulative PnL
- Max Drawdown
- Sharpe Ratio
- CAGR (Compounded Annual Growth Rate)

---

## 7. Outputs

All saved in `outputs/plots/`, including:

- Accuracy trend plots
- Sharpe ratio over time
- Rolling heatmaps
- Cumulative return charts

---

## 8. Results

### ✅ Final Model: Random Forest

| Metric                     | Value          |
| -------------------------- | -------------- |
| Confident Accuracy         | ~85%           |
| Sharpe Ratio               | 13.91          |
| Max Drawdown               | -0.08%         |
| CAGR                       | 4975.69%       |
| Confident Prediction Share | ~2.5% of data  |

>  Confident thresholding significantly improved model precision and risk-adjusted returns.

---

## 📦 Installation

```bash
git clone https://github.com/rupam1123/Alternative-Data-Alpha-Mining.git
cd Alternative-Data-Alpha-Mining

# Install dependencies
pip install -r requirements.txt

# Git LFS (if needed)
git lfs install
git lfs pull
```

