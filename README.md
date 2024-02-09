# stock_price_prediction_one_day_in_the_future


This project focuses on the prediction of the closing price of stocks based on the closing prices of
the past 60 trading days, in which two stocks will be the scope of this project, Apple stock, and
Exxon Mobile stock; where Apple stock is volatile, and Exxon Mobile stock is relatively stable. I
will be applying data preprocessing methods on the two datasets which are provided by Yahoo
Finance API and then creating 4 LSTM models, 2 for each stock where one is a baseline model,
and the other is the optimized model (tuned hyperparameters), and then comparing the effect of the
volatility of the stock on the performance of the models and evaluating each model based on
performance metrics such as adjusted coefficient of determination (adj 𝑅2), Mean Squared Error,
Root Mean Squared Error, Mean Absolute percentage error, And measuring the accuracy of the
predictions that fall within 5, 3, and 1.5 percent from the actual stock price.

Results

Adjusted R Squared 

The Adjusted R squared will be used as the first evaluation metric to compare the four models. Adjusted R2 has been calculated using the test dataset.  In the table below, we can see the adjusted R2 score for each of the four models:
![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/ff878b69-fb97-4269-9092-ea08ea8be86e)

 
Table 5 adjusted R squared of the models
We can see from table 5 that the best model based on adj R squared is the Exxon Mobile tuned model followed by the Apple tuned model. We can also see that the tuned (optimal) models always perform better than the baseline models. Adjusted R2 of 0.9937 means that 99.37% of the variation of the dependent variable (closing price of the 61st trading day) is explained by the independent variables (the set of closing prices for 60 trading days). The Apple tuned model and the Exxon Mobile tuned model will be examined since they were the best two models based on Adjusted R Squared.
4.2	MSE Loss
![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/09f35afb-d278-438c-92c9-8a52c9fb20ad)

Figure 19 Training loss vs. Validation loss for Apple optimal model
 ![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/0143ec58-3a8e-4c14-805e-62d49f71d10c)

Figure 20 Training loss vs. Validation loss for Exxon Mobile optimal model
Figures 19 and 20 display the Training loss (green line) and the Validation loss (blue line) of each optimal model; as we can see, the Apple optimal model fits very well as the generalization gap between the Validation loss curve and the Training loss curve is relatively small. The Exxon mobile tuned model is a bit overfitting; that is, the validation loss is most of the time higher than the training loss, but in overall, it is doing well because when the model was stopped training, both curves were almost at the same point. The validation loss when the Apple tuned model was stopped was 8.33e-07 (best validation loss), while the best validation loss for the Exxon mobile tuned model was 5.3e-05. This means that the Apple tuned model performed better than the Exxon Mobile tuned model on the validation dataset.
4.3	Denormalized Predictions on Test Data
![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/229e735d-cdcb-4707-bf61-68a0d3648d00)


Figure 21 Denormalized predicted Apple stock closing prices
 ![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/14a6e1fb-3747-473c-85d6-8152557274e8)

Figure 22 Denormalized predicted Exxon Mobile stock closing prices
The predicted closing price was denormalized, which we receive during the backtest with
our LSTM models; the reason why this has to be done is that, as described earlier, all input values had to be normalized to the LSTM models. In figures 21 and 22, we can see the LSTM model’s prediction for the closing price (green line) compared to the actual closing price (blue line), and also we can see also that the denormalized predicted closing prices of the Exxon Mobile model were closer to the actual closing prices than the denormalized predicted closing prices of the Apple model.
4.4	Accuracy, MAPE, and RMSE of the Predictions Based on Test Data
As it was mentioned earlier, the accuracy was measured based on three margins of errors from the actual closing price, which were: 5%, 3%, and 1.5%. 
In the Apple stock tuned model, 88.59% of all predicted prices fall within ±5% from the actual closing prices, and 71.25% fall within ±3% from the actual closing prices, while only 40.79% fall within ±1.5% from the actual closing prices. The MAPE was 2.39%, and the RMSE was 2.647, which means that the average distance from actual closing prices was 2.647 dollars.
In the Exxon Mobile stock tuned model, 98.02% of all predicted closing prices fall within ±5% from the actual closing prices, and 92.14% fall within ±3% from the actual closing prices, while only 69.52% fall within ±1.5% from the actual closing prices. The MAPE was 1.29%, and the RMSE was 1.266, which means that the average distance from actual closing prices was 1.266 dollars.
These are big improvements compared to the baseline models which in the case of Apple stock, 37.13% of the predicted closing prices fall within ±5% from the actual closing prices and 20.29% fall within ±3% from the actual closing prices, while only 9.62% fall within ±1.5% from the actual closing prices. The MAPE was 9.27%, and the RMSE was 2.647, which means that the average distance from actual closing prices was 12.57 dollars.
While in the case of Exxon mobile stock, 66.39% of the predicted closing prices fall within ±5% from the actual closing prices and 29.07% fall within ±3% from the actual closing prices, while only 11.62% fall within ±1.5% from the actual closing prices. The MAPE was 9.27%, and the RMSE was 3.86; this means the average distance from actual closing prices was 3.86 dollars.
We can see that from all the numbers stated above that the Exxon Mobile tuned model is the best compared to all other models and that the reason why the Exxon Mobile tuned model is better than the Apple tuned model is that Exxon mobile stock is more stable than the Apple stock which is explained in figure 8.
Note that the RMSE was larger than the MSE in the loss curves because the RMSE is calculated based on denormalized prices while the MSE was calculated based on the normalized prices, and the RMSE and MSE were calculated on different datasets where the RMSE is calculated based on the test dataset while the MSE is calculated based on the validation data set.

4.5	Relation Between Stocks Volatility and APE of Predicted Closing Prices
![image](https://github.com/michelhaj/stock_price_prediction_one_day_in_the_future/assets/36920883/cafe9358-d130-4857-bc78-9ec5e3f9df18)

Figure 23 Volatility and APE of the Apple Tuned Model Predicted Prices

We can see from figure 23 that when the volatility is large, then the Absolute Percentage Error is large as well. At the beginning of 2020, the volatility of the Apple stock closing price was large, and we can see that the APE of the predicted closing price in the model was high at the same period of time (trading days).
 
Figure 24 Volatility and APE of the Exxon Mobile Tuned Model Predicted Prices
As we can see from figure 24, the relation is clear, in the period between 2020 and 2021, the Exxon Mobile stock was relatively volatile, and at the same period, the Absolute Percentage Error of the model’s predicted closing prices was high, as it reached 16% at the point where the volatility was almost 15%. This high volatility in 2020 is probably because of the coronavirus pandemic, which affected all sectors of the financial markets
4.6	Predicting Stock’s Closing Price One Day in the Future
Since the Exxon Mobile tuned model is the best model, the closing price of the Exxon Mobile stock on the trading day 2021-03-15 will be predicted using the Exxon Mobile tuned model given the stock’s Closing prices on the previous sixty trading days.
The actual price was 60.389 dollars, and the predicted closing price was 61.92307 dollars which is a decent estimate of the actual closing price with only a 1.53 dollars difference. This difference is higher than the average distance that was calculated with RMSE when the model was evaluated on the test datasets, which was 1.266 dollars
Depending on the stock and the investor, this estimate might be found by the investor as good if he had no number in his mind about what the closing price of the stock would be in case of a period when the closing price is highly fluctuating.
5	Conclusion

To sum up, everything that has been stated so far, in the introduction, it has been declared that the aim of this research was to predict the closing price of a stock in one of the major stock markets one day in the future based on the closing prices of the past 60 trading days. Two stocks have been introduced, the Apple stock and the Exxon Mobile stock. Whereas four LSTM models were created to make the predictions, two were baseline models, and the other two were optimized (tuned) models. Some important terms concerning computer science, mathematics, and stock analysis have been introduced in the background part. Hence the reader needs a certain aptitude of mathematics to cope with the computer science concepts.
The Exxon Mobile stock has been chosen because it is relatively less volatile compared to the Apple stock. Meaning; on a daily basis, the closing price of Exxon mobile stock had fewer fluctuations compared to the Apple stock closing price, as shown in figure 8.  figures 6 and 7 demonstrate the closing price history of the two models.
Some data preprocessing had been done on the two datasets, such as normalizing and scaling the data to enhance the accuracy and performance of the models, choosing the needed features to work with (the X and Y datasets), and splitting each dataset into training, validation and testing datasets.
The hyperparameter settings of the two baseline models have been introduced. These hyperparameters include the number of layers in the model, the number of cells in each layer, the Dropout rate, the Learning rate of the optimizer, and the number of epochs. Each model was tuned separately; the tuning was based on the MSE of the validation data set. So, each hyperparameter value was chosen such that it had the lowest validation MSE. Figures 9-18 represent how the optimal hyperparameters were chosen.
Then the fitness of the two best models was shown in figures 19 and 20. That is, the generalization of the models was inspected by comparing the validation loss and training loss curves. The Apple tuned model fitted well, but the Exxon Mobile tuned model was overfitting a bit during training, but at the point when the training was stopped, the validation loss was almost the same as the training loss, so, in the end, it also fitted well.
Each model was evaluated on the testing dataset (which had unseen data by the models), and the following performance metrics (statistical measurements) were the base on choosing the best model: Root Mean Squared Error, Adjusted R Squared, Mean Absolute Percentage Error, and accuracy on three different intervals. Whereas Figures 23 and 24 indicate the relation between volatility and the Absolute Percentage Error of the LSTM models. Just using an LSTM model will not help us to minimize the error during volatile periods of the stock because the volatility happens when, e.g., during a financial crisis or if some negative news concerning the company of the stock comes out to the public. Then the LSTM will not be able to predict with high accuracy.

Both Exxon mobile stock baseline and tuned models were performing better on all the stated evaluation metrics than the Apple stock models; the particular reason behind this is that the Exxon Mobile stock was more stable than the Apple stock, which means that the LSTM models require stable stocks to perform at its best.
The tuned Exxon Mobile model was the best model out of the four models as it had the best score in each of the MSE, MAPE, Adj R2, and accuracy, statistical measurements. But the accuracy of the predicted closing price falling in the given interval was decreasing as the interval becomes closer to the actual price (interval becomes smaller). For example, the accuracy of the Exxon Mobile tuned model predictions falling in the interval when the margin of error was 5% from the actual price was 98.02%, and when the margin of error was 3%, it was 92.14%, and finally, when the margin of error was 1.5%, the accuracy was 69.52%.
So, I would say it is foolish to use only the patterns of the past sixty trading days closing prices that have been picked by the LSTM model as a base when investing in stocks, as the financial (stocks) markets are very complex and have many variables that have to be included and taken into consideration when investing. 
The estimates and predictions of the LSTM model alone are not enough to make the investment as it lakes a lot of variables and factors such as macro events, investor sentiment, and market noise, but it can be taken as an initial indication of what the price could be if the trading day closing price was not in a volatile period.
