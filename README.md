# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 25/08/2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
~~~py
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

data = pd.read_csv("/content/air traffic.csv")

# Display available columns for user to choose from
print("Available columns:", data.columns.tolist())

# Select a specific column for time series analysis, e.g., 'Pax'
# Clean the column by removing commas and converting to numeric
time_series = data['Pax'].str.replace(',', '', regex=False).astype(float)

N = len(time_series)

# Define lags
lags = range(35)
# Pre-allocate autocorrelation table
autocorr_values = []

# Mean of the time series
mean_data = np.mean(time_series)
# Variance of the time series
variance_data = np.var(time_series)

# Go through lag components one-by-one
for lag in lags:
  if lag == 0:
    autocorr_values.append(1)
  else:
    # Calculate autocovariance for the given lag
    auto_cov = np.sum((time_series[:-lag] - mean_data) * (time_series[lag:] - mean_data)) / N
    # Normalize by variance to get autocorrelation
    autocorr_values.append(auto_cov / variance_data)

# Display the graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title('Autocorrelation of Pax Data')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
~~~
### OUTPUT:

<img width="1797" height="814" alt="Screenshot 2026-08-04 234639" src="https://github.com/user-attachments/assets/8351959d-06dc-47da-9bc6-908bea77a0fe" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
