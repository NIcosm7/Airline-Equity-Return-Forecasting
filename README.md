# Airline Equity Return Forecasting

Forecasting 30-day airline stock returns using risk measures, Fama-French factors, and airline cancellation data.

## Project Overview

This project analyzes if airline cancellation data can improve equity return forecasts.

The analysis focuses on five major airlines:

- AAL — American Airlines
- DAL — Delta Air Lines
- UAL — United Airlines
- LUV — Southwest Airlines
- ALK — Alaska Air Group

The project first builds a baseline forecasting model using historical stock returns, risk measures, and Fama-French factors. A second model then adds airline cancellation rates to test if cancellation rates help improve the model.

The models predict each airline's forward 30 day stock return.

## Data Sources

The project uses:

- Historical stock price data from Yahoo Finance
- Fama-French three-factor data from Kenneth French's Data Library
- Airline cancellation data from the U.S. Bureau of Transportation Statistics (BTS)

Because downloading the full BTS dataset takes a large amount of time, the processed cancellation data is included in the repository.

## Risk Measures

Three risk measures are calculated for each airline.

### Trailing 30-Day Annualized Volatility

Measures recent overall stock price variability using the previous 30 trading days and annualizes the result.

### Trailing 30-Day Annualized Downside Volatility

Looks at only the negative daily returns. Positive returns are set to zero before calculating downside risk over the previous 30 trading days.

### 252-Day Rolling Beta

Measures each airline stock's sensitivity to the overall market using one year of data.

## Fama-French Three-Factor Analysis

The project uses the Fama-French three-factor model:

$$
R_{\text{airline}} - R_f =
\alpha +
\beta_M(\text{Mkt-RF}) +
\beta_S(\text{SMB}) +
\beta_H(\text{HML}) +
\epsilon
$$

Where:

- Mkt-RF measures excess market returns
- SMB measures the return difference between small-cap and large-cap stocks
- HML measures the return difference between value and growth stocks
- Alpha represents returns not explained by the three factors
- R squared measures how much variation in airline returns is explained by the model

All five airlines had market betas above 1, showing that airline equities were sensitive to market movements.

The Fama-French regressions produced R-squared values of approximately 0.33 to 0.42, meaning the three factors explained roughly 33% to 42% of the variation in daily airline returns.


## Forward 30-Day Return

The forecasting target is the forward 30-day return:

$$
R_{t,t+30} = \frac{P_{t+30}}{P_t} - 1
$$

This represents the percentage return of an airline stock over the next 30 trading days.


## Forecasting Models

Two ordinary least squares regression models are compared.

### Baseline Model

The baseline model includes:

- 30-day annualized volatility
- 30-day downside volatility
- 252-day rolling beta
- Mkt-RF
- SMB
- HML

### Cancellation Model

The second model includes all baseline variables plus:

- Airline cancellation rate


## Model Evaluation

The models are evaluated using:

### Mean Absolute Error

Measures the average absolute difference between predicted and actual 30-day returns.

### Root Mean Squared Error

Measures prediction error.

### Directional Accuracy

Measures how often the model correctly predicts whether the airline stock will increase or decrease over the next 30 trading days.

## Results

Overall, adding cancellation rates did not consistently improve forecasting performance.

For MAE, the cancellation model slightly improved performance for AAL, DAL, and ALK, while performing worse for UAL and LUV.

For RMSE, the cancellation model slightly improved performance for AAL and DAL, while performing worse for UAL, LUV, and ALK.

Directional accuracy was higher for the baseline model. The baseline model performed better for AAL, DAL, UAL, and LUV, while ALK was the only airline where cancellation data slightly improved directional accuracy.

DAL produced the strongest directional accuracy at approximately 62% in the baseline model.

LUV produced the lowest overall forecast errors, with a baseline MAE of approximately 9.0% and RMSE of approximately 11.4%.

## Conclusion

The results suggest that airline cancellation rates provide limited additional predictive value for 30 day airline stock returns once broader market factors and recent risk measures are already included.

Although cancellations are a relevant measure of airline operational success, they did not consistently improve forecasting accuracy.


