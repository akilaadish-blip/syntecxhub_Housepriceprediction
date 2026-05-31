# syntecxhub_Housepriceprediction
# 🏡 House Price Prediction — Linear Regression

An **interactive, browser-based ML pipeline** that walks through every step of building a Linear Regression model on the California Housing dataset — from raw data exploration to live predictions — all running in a single HTML file with no dependencies.

![ML Pipeline](https://img.shields.io/badge/ML-Linear%20Regression-00e5a0?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-California%20Housing-3b82f6?style=flat-square)
![R²](https://img.shields.io/badge/R%C2%B2-0.606-f59e0b?style=flat-square)
![RMSE](https://img.shields.io/badge/RMSE-0.7455-f59e0b?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-64748b?style=flat-square)

-----

## 📸 Demo

Open `house-price-prediction.html` directly in any modern browser — no server, no install, no dependencies.

-----

## 🚀 Features

- **Step-by-step ML pipeline** with 6 interactive stages, each with a “Run Cell” button
- **Simulated Python code blocks** (sklearn syntax) rendered with syntax highlighting
- **Live prediction form** — input custom values and get instant price estimates with 95% CI
- **Scatter plot** — Actual vs. Predicted visualization rendered on HTML Canvas
- **Coefficient bar chart** — visual breakdown of feature importance
- **Regression equation** — full formula with intercept and all feature weights
- **Responsive dark UI** — works on desktop and mobile

-----

## 🔬 Pipeline Steps

|Step|Name                |Description                                                                                   |
|----|--------------------|----------------------------------------------------------------------------------------------|
|1   |**Load & Explore**  |Load California Housing dataset, inspect shape, features, and summary statistics              |
|2   |**Clean & Features**|Check nulls, cap outliers at 99th percentile, engineer `rooms_per_person` and `bedrooms_ratio`|
|3   |**Train Model**     |80/20 train-test split, StandardScaler normalization, LinearRegression fit                    |
|4   |**Evaluate**        |Compute RMSE, R², MAE; render Actual vs. Predicted scatter plot                               |
|5   |**Coefficients**    |Display full regression equation and animated feature importance bars                         |
|6   |**Predict & Save**  |Run example predictions, show model artifacts, enable live prediction form                    |

-----

## 📊 Model Performance

|Metric          |Value               |
|----------------|--------------------|
|R² Score        |**0.606**           |
|RMSE            |**0.7455** ($74,550)|
|MAE             |~0.53 ($53,000)     |
|Train/Test Split|80% / 20%           |
|Scaler          |StandardScaler      |

-----

## 🔍 Key Findings

- **`MedInc` (Median Income)** is the strongest positive predictor of house value — higher income areas → higher prices
- **`Latitude` / `Longitude`** carry large negative coefficients — geography captures the California coastal premium
- **`bedrooms_ratio`** (bedrooms ÷ rooms) is negatively correlated — a high ratio indicates cramped units, reducing value

-----

## 🗂️ Dataset

**California Housing Dataset** (via `sklearn.datasets.fetch_california_housing`)

- **20,640 samples**, **8 original features** + 2 engineered
- Target: `MedHouseVal` — median house value in $100,000 units

|Feature           |Description                             |
|------------------|----------------------------------------|
|`MedInc`          |Median income in block group            |
|`HouseAge`        |Median house age in block group         |
|`AveRooms`        |Average number of rooms per household   |
|`AveBedrms`       |Average number of bedrooms per household|
|`Population`      |Block group population                  |
|`AveOccup`        |Average number of household members     |
|`Latitude`        |Block group latitude                    |
|`Longitude`       |Block group longitude                   |
|`rooms_per_person`|*(Engineered)* AveRooms / Population    |
|`bedrooms_ratio`  |*(Engineered)* AveBedrms / AveRooms     |

-----

## 🛠️ Tech Stack

|Layer         |Technology                                 |
|--------------|-------------------------------------------|
|UI            |HTML5, CSS3 (custom properties, animations)|
|Logic         |Vanilla JavaScript (ES6+)                  |
|Visualization |HTML Canvas API                            |
|Fonts         |Space Mono, DM Sans (Google Fonts)         |
|ML (simulated)|sklearn-style Python shown in code blocks  |


> The model coefficients and scaler parameters are pre-computed and embedded in the JS — the browser runs a faithful JS approximation of the trained Linear Regression.

-----

## 📁 File Structure

```
house-price-prediction/
└── house-price-prediction.html   # Entire app — self-contained, no build step
```

-----

## ⚡ Getting Started

```bash
# Clone the repo
git clone https://github.com/your-username/house-price-prediction.git

# Open in browser (no server needed)
open house-price-prediction.html
```

Or just download the HTML file and double-click it.

-----

## 🧩 How to Extend

Want to swap in a real Python backend?

```python
from sklearn.datasets import fetch_california_housing
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
import pickle

housing = fetch_california_housing(as_frame=True)
df = housing.frame

# Feature engineering
df['rooms_per_person'] = df['AveRooms'] / df['Population']
df['bedrooms_ratio']   = df['AveBedrms'] / df['AveRooms']

features = ['MedInc','HouseAge','AveRooms','AveBedrms',
            'Population','AveOccup','Latitude','Longitude',
            'rooms_per_person','bedrooms_ratio']

X, y = df[features], df['MedHouseVal']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

scaler = StandardScaler()
X_train_s = scaler.fit_transform(X_train)
X_test_s  = scaler.transform(X_test)

model = LinearRegression().fit(X_train_s, y_train)

# Save artifacts
pickle.dump(model, open('house_price_model.pkl', 'wb'))
pickle.dump(scaler, open('scaler.pkl', 'wb'))
```

-----

## 📄 License

MIT — free to use, modify, and distribute.

-----

## 🙌 Acknowledgements

- [California Housing Dataset](https://scikit-learn.org/stable/datasets/real_world.html#california-housing-dataset) — Pace, R. Kelley and Ronald Barry, 1997
- [scikit-learn](https://scikit-learn.org/) — ML in Python