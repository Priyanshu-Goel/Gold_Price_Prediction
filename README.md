# Gold Price Movement Prediction (Hybrid Model)

## Project Overview
This project predicts short-term movements in gold prices in India using global financial indicators, market sentiment, and macroeconomic variables.

Instead of predicting absolute prices, the model forecasts daily percentage change (returns) in gold prices. This improves stability and avoids data leakage.

## Business Context
Gold prices in India are influenced by multiple external factors including global gold prices, USD–INR exchange rates, stock market movements, volatility, and inflation indicators.

Use cases include investment decision-making, hedging strategies, and market risk analysis.

## Data Used

### Market Data
- Gold price (USD/oz)
- USD–INR exchange rate
- NIFTY 50 index
- VIX (Volatility Index)
- Crude oil prices

### Macro Data
- Interest rates (India and US bond yields)
- Inflation proxy variables

## Key Design Decision
The model predicts daily returns instead of gold prices.

Gold price depends on USD gold price and USD–INR exchange rate, which can introduce data leakage if modeled directly. Returns are more stable and better suited for modeling market behavior.

## Feature Engineering

### Lag Features
- lag_1, lag_2, lag_7  
Captures delayed market reactions.

### Rolling Features
- Moving averages (7-day, 14-day)
- Volatility (standard deviation)
- Momentum  
Captures trend, stability, and direction.

### Interaction Features
- Gold × USDINR
- VIX × NIFTY  
Captures relationships between variables.

## Modeling Approach

### SARIMAX
Captures time dependency, trend, and sequential patterns in the data.

### XGBoost
Captures nonlinear relationships and complex feature interactions.

## Hybrid Model
The final model combines SARIMAX and XGBoost.

Step 1: SARIMAX predicts gold returns  
Step 2: Residuals are calculated (Actual - SARIMAX prediction)  
Step 3: XGBoost is trained on residuals  
Step 4: Final prediction = SARIMAX + XGBoost  

## Why Hybrid Model Works
SARIMAX captures time structure but misses nonlinear effects.  
XGBoost captures nonlinear patterns but lacks time awareness.  
The hybrid model combines both strengths.

## Model Evaluation
Evaluation metrics used:
- RMSE (Root Mean Squared Error)
- MAE (Mean Absolute Error)

MAPE was avoided due to instability with near-zero values.

## Results

XGBoost:
- RMSE: 0.017
- MAE: 0.013

Hybrid Model:
- RMSE: 0.0078
- MAE: 0.0069

The hybrid model reduced prediction error by approximately 50%.

## Interpretation
Gold prices are strongly influenced by stock market movements (NIFTY), market volatility (VIX), and global gold trends.

The results support the role of gold as a safe-haven asset.

## Limitations
Financial markets are inherently noisy and unpredictable.  
Sudden market movements due to news or global events are difficult to capture.  
The dataset is limited to approximately 1.5 years.

## Conclusion
This project demonstrates a financial forecasting pipeline integrating macroeconomic and market data with hybrid modeling techniques to improve predictive accuracy.

## One-Line Summary
Built a hybrid time-series and machine learning model to forecast daily gold price movements using macroeconomic and financial indicators, achieving significant improvement in prediction accuracy.
