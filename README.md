# NIFTY 50 Index Price Prediction

## Overview

This project involves predicting the NIFTY 50 index price one week in advance using machine learning algorithms. The model uses historical data, including NIFTY 50 prices, gold and oil prices, bank interest rates, and pre-calculated indicators. Two different machine learning algorithms—RandomForest and LightGBM—are employed, and their predictions are averaged for improved accuracy.

## Data Sources

The following data sources are used in this project:

- **NIFTY 50 Index Prices**: Includes Close, High, Low, and Open prices.
- **Gold Prices**: Daily prices of gold.
- **Oil Prices**: Daily prices of oil.
- **Bank Interest Rates**: Interest rates data from banks.
- **Pre-calculated Indicators**: Various indicators provided in the dataset, including RSI (Relative Strength Index) and Volatility indicators.

## Project Workflow

### 1. Exploratory Data Analysis (EDA)

The first step is to explore the data to understand its structure and relationships. Key insights include:

- **Close Price vs. Next Week’s Close Price**: A scatter plot reveals the relationship between the closing prices and their subsequent week's closing prices.
- **Gold Price vs. Next Week’s Close Price**: A scatter plot indicates a logarithmic relationship between gold prices and the NIFTY 50 index.
- **RSI Indicator**: The histogram of the RSI7 indicator suggests that the NIFTY 50 index is relatively stable.
- **Volatility Indicator**: The histogram shows that the index is rarely volatile, reinforcing its stability.

### 2. Feature Engineering

New features are created to enhance the prediction capabilities of the model:

- **VolumeMulti**: A combination of volume difference and RSI indicators.
- **PriceVolume**: The product of shares traded and the difference between Close and Open prices.

### 3. Model Building

Two different machine learning algorithms are implemented:

#### a. **RandomForest Regressor**
- **Library**: scikit-learn
- **Parameters**:
  - `n_estimators=10`: Number of trees in the forest.
  - `max_depth=8`: Maximum depth of each tree.
  - `criterion='mae'`: Mean Absolute Error as the criterion for splitting.

- **Performance**: The model shows a Mean Absolute Error (MAE) of 77.80 on the validation set.

#### b. **LightGBM Regressor**
- **Library**: LightGBM (developed by Microsoft)
- **Parameters**:
  - `boosting_type='gbdt'`: Gradient Boosting Decision Tree.
  - `objective='poisson'`: Poisson objective function.
  - `metric='mae'`: Mean Absolute Error as the evaluation metric.
  - `num_leaves=100`: Number of leaves in one tree.
  - `feature_fraction=0.99`: Fraction of features used in building trees.

- **Performance**: The model achieves a lower MAE of 21.70 on the validation set, indicating better performance compared to RandomForest.

### 4. Model Ensemble

The predictions from both models are averaged to enhance the overall prediction accuracy:

```python
x_valid['preds'] = (clf_preds + forest_preds) / 2
