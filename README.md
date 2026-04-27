# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 27.04.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv('liver_patient_dataset.csv')

# Create a synthetic time index
data['Date'] = pd.date_range(start='2020-01-01', periods=len(data), freq='D')
data.set_index('Date', inplace=True)

# Use TB column as time series
ts = data['TB']

# REGULAR DIFFERENCING
data['tb_diff'] = ts - ts.shift(1)

# SEASONAL DECOMPOSITION
result = seasonal_decompose(ts, model='additive', period=12)
data['tb_seasonal_adjusted'] = result.resid

# LOG TRANSFORMATION
data['tb_log'] = np.log(ts)
data['tb_log_diff'] = data['tb_log'] - data['tb_log'].shift(1)

# Seasonal decomposition on log-differenced data
result_log = seasonal_decompose(data['tb_log_diff'].dropna(), model='additive', period=12)
data['tb_log_seasonal_diff'] = result_log.resid

# PRINT OUTPUTS
print("REGULAR DIFFERENCING:")
print(data['tb_diff'].dropna().head())

print("\nSEASONAL ADJUSTMENT:")
print(data['tb_seasonal_adjusted'].dropna().head())

print("\nLOG TRANSFORMATION:")
print(data['tb_log_diff'].dropna().head())

# PLOTTING
plt.figure(figsize=(16, 12))

plt.subplot(3, 1, 1)
plt.plot(ts, label='Original')
plt.legend()
plt.title('Original Data')

plt.subplot(3, 1, 2)
plt.plot(data['tb_diff'], label='Regular Differencing')
plt.legend()
plt.title('Regular Differencing')

plt.subplot(3, 1, 3)
plt.plot(data['tb_log_diff'], label='Log Differencing')
plt.legend()
plt.title('Log Transformation')

plt.tight_layout()
plt.show()
```

### OUTPUT:

<img width="413" height="462" alt="image" src="https://github.com/user-attachments/assets/ff6291c3-d334-475f-84fd-8b22ada3e3c4" />


REGULAR DIFFERENCING:

<img width="1022" height="260" alt="image" src="https://github.com/user-attachments/assets/b915c388-8b23-4fed-8f75-1248d130451f" />


SEASONAL ADJUSTMENT:

<img width="990" height="231" alt="image" src="https://github.com/user-attachments/assets/3f2dd903-2503-4020-bdc3-7e676eace209" />


LOG TRANSFORMATION:

<img width="1006" height="266" alt="image" src="https://github.com/user-attachments/assets/78d75fb5-133d-4509-9a1f-7a781dda2ded" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
