# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 22/04/26
# Name: Isaac Raja T
# Reg No: 212224040123

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('Truck_sales.csv')

data['Month-Year'] = pd.to_datetime(data['Month-Year'], format='%y-%b', errors='coerce')
data = data.dropna(subset=['Month-Year'])

data.set_index('Month-Year', inplace=True)

sales_col = 'Number_Trucks_Sold'

data['sales_diff'] = data[sales_col] - data[sales_col].shift(1)

result = seasonal_decompose(data[sales_col], model='additive', period=12)
data['sales_sea_diff'] = result.resid

data['sales_log'] = np.log(data[sales_col])

data['sales_log_diff'] = data['sales_log'] - data['sales_log'].shift(1)

result = seasonal_decompose(data['sales_log_diff'].dropna(), model='additive', period=12)
data['sales_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data[sales_col], label='Original')
plt.legend(loc='best')
plt.title('Original Data')

plt.subplot(6, 1, 2)
plt.plot(data['sales_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(data['sales_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')

plt.subplot(6, 1, 4)
plt.plot(data['sales_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')

plt.subplot(6, 1, 5)
plt.plot(data['sales_log_diff'], label='Log + Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing')

plt.subplot(6, 1, 6)
plt.plot(data['sales_log_seasonal_diff'], label='Log + Diff + Seasonal')
plt.legend(loc='best')
plt.title('Log + Differencing + Seasonal Adjustment')

plt.tight_layout()
plt.show()
```


### OUTPUT:


REGULAR DIFFERENCING:
<img width="1322" height="219" alt="image" src="https://github.com/user-attachments/assets/20908aa6-14bf-4945-88a6-1cac7b33533e" />



SEASONAL ADJUSTMENT:
<img width="1319" height="216" alt="image" src="https://github.com/user-attachments/assets/758dd06b-1950-4103-ad24-a76b6a7d74dd" />



LOG TRANSFORMATION:
<img width="1323" height="658" alt="image" src="https://github.com/user-attachments/assets/2a3d80e4-4d06-48b6-b844-02157669a59b" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
