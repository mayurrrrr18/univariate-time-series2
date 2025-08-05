# univariate-time-series2
"Analysis and forecasting using SARIMAX on univariate time series data
Step 1: Data Preparation and Visualization
I will load the Electric_Production.csv file, rename the columns for clarity, and convert the DATE column to a datetime index. I'll then visualize the time series and perform a decomposition to explicitly show the trend and seasonal components.

<img width="1600" height="747" alt="image" src="https://github.com/user-attachments/assets/6dfcb52d-ca85-4904-b626-cc910736dc6b" />

The visualizations and the ADF test on the original data confirmed a clear trend, strong seasonality, and non-stationarity. A standard ARIMA model would not be sufficient. Therefore, we will use a SARIMAX model, which can handle both non-seasonal and seasonal components.

Step 2: Differencing for Stationarity (Continued)
I will now create a new series with both regular and seasonal differencing applied. Then, I will confirm its stationarity with an ADF test and visualize the ACF and PACF plots to determine the model's parameters.

<img width="1600" height="747" alt="image" src="https://github.com/user-attachments/assets/3c66e31f-1ded-4351-b35a-6467cfb26138" />
<img width="1600" height="1280" alt="image" src="https://github.com/user-attachments/assets/b138bfbf-b3e5-4d04-ab82-87819535027e" />


The differencing operation was successful, and the ADF test confirmed that the series is now stationary. The ACF and PACF plots on the twice-differenced data allow us to determine the non-seasonal and seasonal parameters for our SARIMAX model.

Step 3: Identifying the SARIMA Parameters (p,d,q,P,D,Q,S)
Non-seasonal parameters:

The PACF plot shows a significant spike at lag 1, suggesting p=1.

The ACF plot also shows a significant spike at lag 1, suggesting q=1.

We used one order of regular differencing, so d=1.

Seasonal parameters:

The ACF plot shows a significant spike at the seasonal lag (lag 12), suggesting a seasonal MA component of order 1 (Q=1).

The PACF plot shows a significant spike at lag 12, suggesting a seasonal AR component of order 1 (P=1).

We used one order of seasonal differencing, so D=1.

The seasonal period is 12, so S=12.

Based on this, we will build a SARIMAX(1, 1, 1)(1, 1, 1, 12) model.

Step 4: Building, Training, and Evaluating the SARIMAX Model
I will now split the data into a training and testing set to evaluate the model's performance. Then, I will fit the SARIMAX model, make predictions on the test set, and calculate the Root Mean Squared Error (RMSE) to assess its accuracy.

Step 5: Forecasting Future Production
Finally, I will use the trained model to forecast the monthly electric production for the next 24 months.

<img width="1600" height="747" alt="image" src="https://github.com/user-attachments/assets/d28e6720-d5f4-4496-bd24-c4707db4b8f9" />

<img width="1600" height="747" alt="image" src="https://github.com/user-attachments/assets/86d63851-0580-4cf9-9692-9e1026552db9" />





Following the same process as the previous analysis, I have performed a similar time series analysis on the Electric_Production.csv dataset, this time using a SARIMAX model to account for the clear seasonal patterns.

Step 1: Data Preparation and Visualization
First, I loaded the data, renamed the columns to Date and Production, and set the date as the index. The initial plot below shows a strong upward trend and a clear, repeating seasonal pattern, with production peaking in the summer months.

The time series decomposition further illustrates these components, clearly separating the trend, the 12-month seasonal cycle, and the remaining residuals.

Step 2: Checking for Stationarity and Differencing
To check for stationarity, I first performed an Augmented Dickey-Fuller (ADF) test on the original data.

ADF Test on Original Data: The p-value was 0.186, which is greater than 0.05, confirming that the series is non-stationary.

Differencing: Due to the presence of both a trend and seasonality, I applied both a regular first-order difference and a seasonal difference (with a period of 12) to the data. This removed the trend and the seasonal cycle.

ADF Test on Differenced Data: The p-value for the twice-differenced series was 2.06
times10 
−12
 , which is far below 0.05, confirming that the series is now stationary.

Step 3: Identifying the SARIMA Parameters (p,d,q,P,D,Q,S)
From the ACF and PACF plots on the stationary, differenced data, I determined the parameters for the SARIMAX model:

Non-seasonal parameters: Based on the significant spikes at lag 1, I chose p=1 and q=1. The differencing step gives us d=1.

Seasonal parameters: The plots showed significant spikes at the seasonal lag (lag 12), leading to the selection of P=1 and Q=1. The seasonal differencing step gives us D=1, with the monthly seasonality giving S=12.

This resulted in a SARIMAX(1, 1, 1)(1, 1, 1, 12) model.

Step 4: Model Building and Evaluation
I split the data into training and test sets. The SARIMAX model was trained on the training data and evaluated on the test data.

Model Summary: The Ljung-Box test p-value of 0.57 suggests the model residuals are not significantly different from white noise, which is a good indicator of a well-fitted model.

Evaluation: The Root Mean Squared Error (RMSE) on the test set was 4.41, indicating that the model's predictions were, on average, very close to the actual values. The plot below shows how closely the model's forecasts track the actual test data.

Step 5: Forecasting Future Production
Finally, I used the fitted model to forecast monthly electric production for the next 24 months. The plot below shows the historical data along with the future forecast, which successfully captures the expected seasonal patterns for the coming years.










































































































