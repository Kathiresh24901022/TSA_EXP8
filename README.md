# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 29/05/2026

### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings

from statsmodels.tsa.holtwinters import ExponentialSmoothing

data = pd.read_csv("Google_Stock_Price_Test.csv");
data['Date'] = pd.to_datetime(data['Date'], format='mixed')

data = data.sort_values('Date')
data.set_index('Date', inplace=True)
data = data[['Close']]
print("Shape of Dataset:", data.shape)

print("\nFirst 20 Rows:\n")

print(data.head(20))

plt.rcParams['figure.figsize'] = (12,6)
warnings.filterwarnings("ignore")

plt.figure(figsize=(12,6))

plt.plot(data['Close'].head(50),
         label='Original Data')

plt.title("First 50 Google Stock Prices")

plt.xlabel("Date")

plt.ylabel("Close Price")

plt.legend()

plt.grid()

plt.show()

data['Rolling_Mean_5'] = data['Close'].rolling(window=5).mean()

print("\nRolling Mean (Window = 5)\n")

print(data['Rolling_Mean_5'].head(10))

data['Rolling_Mean_10'] = data['Close'].rolling(window=10).mean()

plt.figure(figsize=(12,6))

plt.plot(data['Close'],
         label='Original Data')

plt.plot(data['Rolling_Mean_5'],
         label='Moving Average (5)')

plt.plot(data['Rolling_Mean_10'],
         label='Moving Average (10)')

plt.title("Moving Average Model - Google Stock Price")

plt.xlabel("Date")

plt.ylabel("Close Price")

plt.legend()

plt.grid()

plt.show()

model = ExponentialSmoothing(
    data['Close'],
    trend='add',
    seasonal=None
)

fit_model = model.fit()

data['Exponential_Smoothing'] = fit_model.fittedvalues

plt.figure(figsize=(12,6))

plt.plot(data['Close'],
         label='Original Data')

plt.plot(data['Exponential_Smoothing'],
         label='Exponential Smoothing')

plt.title("Exponential Smoothing - Google Stock Price")

plt.xlabel("Date")

plt.ylabel("Close Price")

plt.legend()

plt.grid()

plt.show()
```
### OUTPUT:


Moving Average

<img width="877" height="708" alt="image" src="https://github.com/user-attachments/assets/a88eed34-bb51-48be-80ad-2e28ea42d6f7" />

Plot Transform Dataset

<img width="707" height="622" alt="image" src="https://github.com/user-attachments/assets/09af41e5-981d-4c65-b7a6-e29913989960" />

Exponential Smoothing

<img width="847" height="465" alt="image" src="https://github.com/user-attachments/assets/2e6ee7b1-cd8a-4e97-8af5-aa64ad32f7e6" />

### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
