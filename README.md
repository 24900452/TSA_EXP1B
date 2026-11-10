# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date:20.10.2026 

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

data = pd.read_csv('/content/nifty_it_index.csv')
data.head()

data['Date'] = pd.to_datetime(data['Date'])

data.set_index('Date', inplace=True)

price = 'Close'

data['price_diff'] = data[price] - data[price].shift(1)

result = seasonal_decompose(data[price], model='additive', period=12)
data['price_sea_diff'] = result.resid


data['price_log'] = np.log(data[price])


data['price_log_diff'] = data['price_log'] - data['price_log'].shift(1)


result = seasonal_decompose(
    data['price_log_diff'].dropna(),
    model='additive',
    period=12
)

data['price_log_seasonal_diff'] = result.resid

<img width="596" height="138" alt="download" src="https://github.com/user-attachments/assets/5cd586da-ba25-455a-a0eb-70cf038a4826" />

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data[price], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('Closing Price')

plt.subplot(6, 1, 2)
plt.plot(data['price_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Price')

plt.subplot(6, 1, 3)
plt.plot(data['price_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted Price')

plt.subplot(6, 1, 4)
plt.plot(data['price_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Closing Price)')

plt.subplot(6, 1, 5)
plt.plot(data['price_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Price))')

plt.subplot(6, 1, 6)
plt.plot(data['price_log_seasonal_diff'],
         label='Log Transformation and Regular Differencing and Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Price)))')

plt.tight_layout()
plt.show()

# Display selected results
data[[price, 'price_diff', 'price_log']].plot(kind='line', figsize=(12, 6))
plt.show()
```

### OUTPUT:
<img width="596" height="138" alt="download" src="https://github.com/user-attachments/assets/ca7d3ba7-685f-4329-af27-f5d9862eed5e" />

REGULAR DIFFERENCING:
<img width="590" height="138" alt="download" src="https://github.com/user-attachments/assets/c5353473-adad-47d0-bf1f-f9b9b6673124" />


SEASONAL ADJUSTMENT:

<img width="602" height="138" alt="download" src="https://github.com/user-attachments/assets/08a77901-1c63-4813-a4d3-7b221d671517" />

LOG TRANSFORMATION:
<img width="574" height="138" alt="download" src="https://github.com/user-attachments/assets/28126298-9c12-4a88-8190-5660879393b1" />

Log Transformation and Regular Differencing:
<img width="595" height="138" alt="download" src="https://github.com/user-attachments/assets/4ca19eec-13e7-44db-9c76-23048ec2eb07" />
Log Transformation, Regular Differencing and Seasonal Differencing:
<img width="641" height="138" alt="download" src="https://github.com/user-attachments/assets/4ae59305-30f6-48bc-b8c4-f7e247c01a73" />

OVERALL VIEW:
<img width="1003" height="498" alt="download" src="https://github.com/user-attachments/assets/c0519dc4-04ce-4930-a9cf-5216728fb195" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
