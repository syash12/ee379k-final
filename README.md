Team 7: Vamsi Ghorakavi, Matt Tawil, Yash Shahi, Sungho Lim

# Predicting Future Sales

For our final Data Science Project, we undertook the opportunity to compete in [this kaggle competition](https://www.google.com/url?q=https://www.kaggle.com/c/competitive-data-science-predict-future-sales&sa=D&ust=1525461654613000&usg=AFQjCNFRtos567F9ntNdD1uYcjDDOlTODQ). This blog post will explore the data, and look at the various methods that we used to try to predict the data. As of writing this blog post, we are currently ranked 71st out of 412 teams with a RMSE score of 1.02364. 

Data Exploration
-----------------
First, we are going to take a deeper look at the data. This dataset contains the sales data of Russian stores products. Specifically, we are looking to predict the sales of 83 different products in November 2015 based on data from January 2013 to October 2015. 

![items per category](https://i.imgur.com/joWAUc1.png)

The above block diagram visualizes numbers of items sold per category.

Generally for for predicting time data, we need the data to be stationary. Meaning that the mean, variance, and covariance should not be a function of time for our data. There is an overall trend that we need to remove for our data to be stationary.

![data breakdown](https://imgur.com/9DNOqwh.png)

This image shows the breakdown of our data. After we remove the overall trend of the data. The data becomes stationary and we are able to predict the data with our models

To test the stationarity of our data, we used the Dickey fuller test. This test will show us if our data is stationary after we removed the overall trend. After the test, the p value was 0.01 meaning that we can assume that our data is stationary and use time series prediction modes.

![dickey fuller test](https://imgur.com/tOAPkVT.png)
 
Training Models
-----------------
We tried out a variety of different models to predict this dataset ranging from ARMA and ARIMA, Prophet, Nested LSTMs, XGBoost, and Independently Recurrent Neural Networks.


#### ARIMA
 
Generally ARMA and ARIMA are the standard way to predict stationary time series. ARIMA (Autoregressive Integrated Moving Average) is generally used to predict stationary time series. As a time series technique, ARIMA assumes there is a continuity in the trend between the past and future. Using ARIMA, we were not really able to predict the sales of the data well. Our RMSE score was around 2.0. 

It is possible that the ARIMA gave us such a bad score was because each product only had ~25 or so data points available.

#### Prophet

 Next we tried to predict the data using prophet. Prophet is a framework to predict time series built by Facebook Data Scientists. While tuning prophet, we were having trouble predicting the overall trend of the data into November. This error could have taken place because we did not tune our model properly. We did not see that much improvement on our overall Score

#### Nested LSTMs
Library used: https://github.com/hannw/nlstm

Afterwards, we tried to predict the series using nested LSTMs. For time series, LSTMs are are more prefered than Neural Networks because they do not have the vanishing gradient issue. The difference between using a recurrent neural network with LSTMs is that the LSTM replaces a neuron in the RNN with a LSTM unit. LSTM units consist of an information cell, an input gate, an output gate and a forget gate. The cell is responsible for "remembering" values over arbitrary time intervals. The gates can be thought of as regulators, controlling the flow of information into the information cell.

This model gave us our best RMSE score of 1.02. We saw that using this type of model gave us a better prediction than traditional time series.

#### Independent Recurrent Neural Networks
Library used: https://github.com/batzner/indrnn

The final model we tried to fit is something called a Independent Recurrent Neural Network. It is another way to try to solve the vanishing gradient issue, but the first paper that we saw on it was written in [March 2018](https://arxiv.org/abs/1803.04831). Using this model we got a RMSE score of 1.03 meaning that it had similar performance to the Nested LSTM.

Conclusion
-----------------
Overall, the models we used to predict our data gave us a RMSE of 1.02. Stacking the working models did not work too well for predicting our data. But we were able to explore many different ways to predict time series. 
