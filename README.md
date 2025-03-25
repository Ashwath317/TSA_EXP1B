# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 24.03.25

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
data = pd.read_csv('AirPassengers.csv')
data.head()
data['Month'] = pd.to_datetime(data['Month']) # data=pd.read_csv("/content/AirPassengers.csv",parse_dates=
data.set_index('Month', inplace=True)
data['passengers_diff'] = data['#Passengers'] - data['#Passengers'].shift(1)
result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)
result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
plt.plot(data['passengers_diff'], label='Differencing')
plt.legend(loc='best')
plt.title('Differencing')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted No of passengers')
plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Difference ')
plt.legend(loc='best')
plt.title('Seasonal Difference')
plt.xlabel('Year')
plt.ylabel('No of passengers')
plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of passengers)')
plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of passengers))')
data['passengers_log_seasonal_diff'] = data['passengers_log_diff'] - data['passengers_log_diff'].shift(12)
plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation and regular Differencing and S')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of passengers)))')
plt.tight_layout()
plt.show()+
data.plot(kind='line')
```
### OUTPUT:

REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/75ec2fa6-a406-4d37-b924-d06c219a49dc)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/ca28ec4f-036e-48e9-8b56-0fe0400b3338)

LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/55c52c72-fef6-400f-b7a1-1a559a194cb8)

LOG TRANSFORMATION AND REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/e5e712cb-63d4-4efc-b504-8d6005b097fb)

LOG TRANSFORMATION,REGULAR DIFFERENCING AND SEASONAL DIFFERENCING:

![image](https://github.com/user-attachments/assets/c091183c-2af1-40ae-9ef1-eef8ed241624)

OVERALL GRAPH:

![image](https://github.com/user-attachments/assets/7cc306ec-d164-4bfa-aefe-247a8e4c0fef)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
