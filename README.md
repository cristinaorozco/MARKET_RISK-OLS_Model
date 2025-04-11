# 📈 OLS Model – Market Risk Analysis for Apple Inc. (AAPL)

This project presents a **statistical linear regression model (OLS)** designed to estimate the stock price of **Apple Inc. (AAPL)** using three key macroeconomic indicators:

- **NASDAQ-100 Index** (`^NDX`)
- **USD Index** (`DX-Y.NYB`)
- **10-Year Treasury Yield** (`^TNX`)

These indicators were selected based on their economic relevance and their low multicollinearity risk. The model aims to explore **macroeconomic-driven variations in AAPL’s price**, offering insights into market risk.

---

## 📊 Project Overview

- **Dependent variable**: AAPL Closing Price
- **Independent variables**:
  - **NASDAQ-100**: Represents the 100 largest non-financial companies listed on Nasdaq.
  - **USD Index**: Measures the strength of the dollar against a basket of major currencies.
  - **10-Year Treasury Yield**: Reflects investor sentiment regarding long-term growth and inflation.

---

## 🧪 Methodology

### 1. **Data Collection**
Historical data was extracted using the [`yfinance`](https://pypi.org/project/yfinance/) library from Yahoo Finance for the period **2024-01-01 to 2025-03-31**.

```python
import yfinance as yf

data_apple = yf.download("AAPL", start="2024-01-01", end="2025-03-31")
data_nasdaq = yf.download("^NDX", ...)
data_usd_index = yf.download("DX-Y.NYB", ...)
data_treasury = yf.download("^TNX", ...)
```

### 2. **Data Preprocessing**
- Reformatted MultiIndex columns
- Renamed variables for clarity
- Merged datasets using the `Date` column
- Flattened column names to ensure single-level indexing

### 3. **Exploratory Data Analysis**
- Used a Pearson correlation matrix
- Verified low multicollinearity with VIF analysis

### 4. **Modeling: Ordinary Least Squares (OLS)**
The model was built using the `statsmodels` library:

```python
from statsmodels.api import OLS, add_constant

X = add_constant(df[['Nasdaq', 'USD_index', '10y_Treasury_Yield']])
y = df['Price_apple']
model = OLS(y, X).fit()
```

---

## 📈 Model Results

### Key Statistics:

| Metric                      | Value     |
|----------------------------|-----------|
| R-squared                  | 0.865     |
| Adjusted R-squared         | 0.863     |
| F-statistic                | 520.5     |
| p-value (model)            | 1.05e-105 |
| Durbin-Watson              | 2.102     |

### Coefficients:

| Variable                | Coefficient | p-value |
|------------------------|-------------|---------|
| Intercept              | -152.6896   | 0.002   |
| Nasdaq                 | +0.0160     | 0.000   |
| USD Index              | +2.2560     | 0.001   |
| 10Y Treasury Yield     | -42.9632    | 0.000   |

### VIF Analysis:

| Variable           | VIF  |
|--------------------|------|
| Nasdaq             | 1.73 |
| USD Index          | 6.04 |
| 10Y Treasury Yield | 4.69 |

✅ All variables have **VIF < 10**, indicating **no serious multicollinearity**.

---

## 📉 Visualizations

- Correlation heatmap
- Actual vs Predicted AAPL price graph

---

## 🔍 Test Case

**Input (2025-04-01):**

- Nasdaq: 19436.42  
- USD Index: 104.26  
- 10Y Treasury Yield: 4.156  

**Prediction:**

```
Predicted AAPL Price = −152.6896 + (0.0160 × Nasdaq) + (2.2560 × USD Index) − (42.9632 × Yield)
                     ≈ $214.95
```

**Actual closing price:** $223.19  
**Absolute Error:** $8.29  
**Percentage Error:** ≈ 3.71%

✅ A relative error < 5% is considered **reasonable** for a model using macro indicators.

---

## ✅ Conclusions

- The model **explains 86.5%** of the variance in AAPL’s stock price.
- All variables are **statistically significant (p < 0.01)**.
- The model **passes multicollinearity checks**.
- Residuals exhibit **no autocorrelation**.
- Excellent performance for a simple, interpretable macro-based model.

---

## 🚀 Next Steps

To improve accuracy:
- Integrate **alternative data** (e.g., news sentiment, earnings).
- Use **non-linear models** (e.g., SVR, Random Forest).
- Test with rolling windows and out-of-sample periods.

---

## 🧠 Author

Cristina Orozco  
Data Scientist | Financial Risk Analyst  
📫 [LinkedIn](https://www.linkedin.com/in/...) | 🌐 [GitHub](https://github.com/...)