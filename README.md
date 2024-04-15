# Time Series Forecasting with a SARIMA Model and an Artificial Neural Network with LSTM cells 

This repository consists of a forecasting project for retail clothing sales. We work with a dataset that contains monthly sales values 
of retail clothing and clothing articles from 1992 to 2020. However, we only work with the segment up to 2019 because the values of the
2020 sales were severely affected by the COVID-19 pandemic, making them unpredictable for any model. This project aimed to create
a model that accurately forecasts future sales values from past data. To do this, we created a SARIMA model and a neural network with LSTM cells.

In preparation for model creation, the following steps were taken:

* Importing and plotting the dataset to observe the yearly trends of retail clothing sales.
* Splitting the data into a training and test set
* Creating a naive forecast to have a baseline to compare model performance

## SARIMA model

After the previous step, we decomposed the training series to obtain its seasonality and trend. With this information, we concluded that the best
model based on autoregression (AR) and moving average (MA) to forecast the series would be a SARIMA model. This is because this model considers both
the seasonality and trend, using them to forecast future values. The creation of the SARIMA model involved the following steps:

* The Augmented Dickey-Fuller (ADF) test was used to determine whether the series was stationary
* After determining the series as non-stationary, we applied seasonal (12th order) differencing to the series stationary
* Stationarity was confirmed with another ADF test, this time on the transformed series
* ACF and PACF plots were created to determine the initial parameters of the series
* Multiple sets of SARIMA parameters were tested, and the Akaike Information Criterion (AIC) was used to determine the optimal one
* The optimal model was used to forecast 2 years into the future (2018 and 2019), outperforming the naive forecast

## Neural network with LSTM cells

Long short-term memory cells (LSTMs) are a form of recurrent neural network (RNN) designed to overcome the vanishing gradient problem and capture 
long-term dependencies. This ability to capture long-term patterns is what makes it popular for forecasting time series. In this project, we used
the TensorFlow library to create a neural network with LSTM cells that was trained on the dataset and used to make forecasts. This process was as follows:

* The training and test sets were divided into windows (sequences) of 12 values that would be used to predict a horizon of 1 (only one future value)
* Different neural networks with varying structures and parameters were built and trained iteratively to find the best composition
* The neural network was then used to forecast sales values from 2018 to 2019, obtaining better performance than naive forecasting and slightly poorer than the SARIMA model
