### Developed By : Shriram S
### Register No. : 212222240098
### Date : 

# Ex.No: 6               HOLT WINTERS METHOD


### AIM:

To create and implement Holt Winter's Method Model using python for Methi vegetable price.



### ALGORITHM:

1. You import the necessary libraries
2. You load a CSV file containing daily sales data into a DataFrame, parse the 'date' column as
datetime, and perform some initial data exploration
3. You group the data by date and resample it to a monthly frequency (beginning of the month
4. You plot the time series data
5. You import the necessary 'statsmodels' libraries for time series analysis
6. You decompose the time series data into its additive components and plot them:
7. You calculate the root mean squared error (RMSE) to evaluate the model's performance
8. You plot the original sales data and the predictions

### PROGRAM:

#### Import Neccesary Libraries
```py
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.holtwinters import ExponentialSmoothing
```

#### Load the dataset

```py

# Load the CSV file
file_path = '/content/prices.csv'
data = pd.read_csv(file_path)

```
```py
# Convert the 'Price Dates' column to datetime format
data['Dates'] = pd.to_datetime(data['Price Dates'], format='%d-%m-%Y')

# Set 'Dates' as the index of the DataFrame
data.set_index('Dates', inplace=True)
data.sort_index(inplace=True)

# Display the first few rows of the dataset to verify
print(data.head())
```
```py
# Select the 'Tomato' prices for analysis and drop any missing values
tomato_prices = data['Tomato'].dropna()

# Plot the original Tomato prices to visualize the data
plt.figure(figsize=(10, 6))
plt.plot(tomato_prices, label='Tomato Prices', color='blue')
plt.title('Tomato Prices Over Time')
plt.xlabel('Date')
plt.ylabel('Price')
plt.grid(True)
plt.legend()
plt.show()
```

#### Split into training and testing sets (80% train, 20% test)

```py
# Split data into training and test sets (80% training, 20% testing)
split_index = int(0.8 * len(tomato_prices))
train_data = tomato_prices[:split_index]
test_data = tomato_prices[split_index:]
# Apply Holt-Winters Exponential Smoothing
model = ExponentialSmoothing(train_data, trend='add', seasonal='add', seasonal_periods=7)
```

#### Fitting the model
```py
fit = model.fit()
# Display the model parameters
print(fit.params)
```

#### Forecast and evaluate

```py
# Forecast for the length of the test data
forecast = fit.forecast(len(test_data))

# Display the forecasted values
print("Forecasted Prices:")
print(forecast)

```

#### Evaluate performance

```py

from sklearn.metrics import mean_absolute_error

# Calculate Mean Absolute Error
mae = mean_absolute_error(test_data, forecast)
print(f"Mean Absolute Error (MAE): {mae:.2f}")

```


#### Plot predictions


```py
# Plotting the training data, test data, and forecast
plt.figure(figsize=(12, 6))
plt.plot(train_data, label='Training Data', color='blue')
plt.plot(test_data, label='Actual Prices', color='green')
plt.plot(forecast, label='Forecasted Prices', color='red', linestyle='--')
plt.title('Tomato Prices Forecast using Holt-Winters Method')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT:

#### Evaluation 

![image](https://github.com/user-attachments/assets/6b3044ad-2b09-4ec5-af62-c9a50d3c835f)



#### TEST PREDICTION

![image](https://github.com/user-attachments/assets/1a2327e7-f034-46a5-8856-7b33d59db244)


#### FINAL PREDICTION

![image](https://github.com/user-attachments/assets/680b290d-a339-4e31-84fb-94e2053ac329)


### RESULT:

#### Thus the program run successfully based on the Holt Winters Method model.
