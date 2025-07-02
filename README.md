#  Alternative Data Alpha Mining using Reddit, News & Google Trends with ML Backtesting

This project explores **alpha generation** using **alternative data sources**—Reddit sentiment, financial news, and Google Trends—to **predict stock returns**. We apply **Random Forest** and **LightGBM** models, introduce **confidence thresholding**, and conduct **rolling-window backtesting** to assess strategy robustness.

---

## 📚 Table of Contents

- [📦 Project Structure](#-project-structure)
- [🧠 Approach](#-approach)
- [💃️ Datasets](#️-datasets)
- [🛠️ Features](#️-features)
- [🤖 Modeling](#-modeling)
- [📊 Backtesting](#-backtesting)
- [📁 Outputs](#-outputs)
- [📈 Results](#-results)
- [📦 Installation](#-installation)
- [🧪 Running the Code](#-running-the-code)
- [🧹 Dependencies](#-dependencies)
- [⚖️ License](#️-license)
- [🙌 Acknowledgements](#-acknowledgements)
- [✍️ Author](#-author)

---

## 📦 Project Structure

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
