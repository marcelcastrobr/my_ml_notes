# Forecasting



## Timeseries 101

**Univariate**: Only one variable is varying over time. For example, data collected from a sensor measuring the temperature of a room every second. Therefore,  each second, you will only have a one-dimensional value, which is the  temperature.

**Multivariate**: Multiple variables are varying over time. For example, a tri-axial  accelerometer. There are three accelerations, one for each axis (x,y,z)  and they vary simultaneously over time.



## Deep Learing-based Forecasting or Neural Forecasting

Leverages deep neural networks to predict time series into the future. It requires less feature engineering compared to classical models such as ARIMA and ETS.

**Problem**: Cold start problem

**Issue**: Forecast articles that have little or no historical sales data.

**Idea**: learn typical behaviour of new articles based on patterns of other types of articles.

**Types of neural forecast**:

- Local models: trained for each time series.
- Global models: trained accross multiple related time series.It can address cold start problem as it uses learned patterns, also known as embeddings, to produce forecasts.

#### Models:

[DeepAR](https://arxiv.org/pdf/1704.04110.pdf): autoregressive model based on RNN (recurrrent neural network) for univariate timeseries. DeepAR produces a probabilistic forecast (i.e. a set of possible outcomes, each with a certain probability). 

## References:

- Blog: [How adidas and AWS optimised supply chain management to satisfy customer  demand through Machine Learning and MLOps on Amazon SageMaker](https://medium.com/adidoescode/how-adidas-and-aws-optimised-supply-chain-management-to-satisfy-customer-demand-through-machine-942eade0de76)

