# Hotel-Cancellation-Prediction

This is an academic project. My teammate and I forecasted cancellation rate for 2 hotels in NYC and ATL. I was responsible for NYC hotel EDA, data handling, and predictions. This repo contains only the models for NYC hotel. The paper write-up includes report of both NYC and ATL hotel. 

In this project, I tried to predict the cancellation rate of an international hotel located in New York city. Since this hotel is of international scale, they have their bookings situation and cancellation pattern very different than middle and small scaled hotels. Their rooms are sold via multiple channels with different kind of contracts. The cancellation patterns also depend greatly on how the bookings were sold. 

<img width="388" alt="Screen Shot 2019-12-20 at 6 29 47 PM" src="https://user-images.githubusercontent.com/45189309/71252101-a758dd80-2356-11ea-9557-f4cfb494cdd7.png">


# Result 

The table below shows results of all models used (Traditional, Regression, KNN, Tree, Random Forest) on training set (In-sample Metrics) and on Testing set (Out-sample Metrics). 


My main metrics is MASE with benchmark is a mean cancellation rate of training set as Naive prediction. The best performing model is Combined Model with the highest percentage of error reduction compared to Naive prediction. 

**Example of result interpretation**: 

MASE: On Testing data, Combined Model reduced 79.03% of prediction error compared to Naive prediction for 1 to 7 days prior to Stay Date (the night when customers stay at the hotel). 

MAPE: On Testing data, Combined Model prediction is off by 2.91% on average in day 1 to 7 prior to Stay Date.

MAE: On Testing data, Combined Model predicted with averaged error of 1.84 bookings that will survive in day 1 to 7 prior to Stay Date.

<img width="581" alt="Screen Shot 2019-12-20 at 6 35 16 PM" src="https://user-images.githubusercontent.com/45189309/71252369-5f868600-2357-11ea-929f-080c0abe0f3b.png">

This is the visualization of predictions on testing data of all models used: 
<img width="869" alt="Screen Shot 2019-12-20 at 6 45 53 PM" src="https://user-images.githubusercontent.com/45189309/71252901-d3755e00-2358-11ea-8983-f46dc5f13e28.png">

# Result Discussion 
For New York hotel, the out-of-sample metrics are usually better than the in-sample metrics. Our models often outperformed Naïve predictions more in testing set than in training set. This can be due to the higher variation nature of the training set than the testing set. 

In general, the predictions for Days Prior closer to Stay Date were better than predictions for longer lead days to Stay Date. Again, the reason can be the high volatility in data and fewer observations the further away from the booked Stay Date. Closer to Stay Date, there are more observations and the pattern might be more prominent and easier for our model to pick up. 

In Days Prior period 01-07, the in-sample metrics and out-sample metrics are very close to each other. The cancellation trend in training and testing set might be similar, which can constitute a last-week effect. Further investigation on the last-week effect might be helpful to understand the last-week cancellation behavior better, and potentially find a way to reduce cancellation in other Day Prior periods. It is possible that there is a policy restricting last-week cancellation, regardless of product type, that can explain for the steady decline in cancellation rate in the last week before Stay Date 
The Traditional Model performed relatively well compared to other sub-learners in days closer to Stay Date while Regression Tree performed better than other sub-learners in Days Priors further from Stay Date. In Days Prior period 01-07, cancellation pattern might be more uniform, hence Traditional model performed particularly well in this time period. In days further away from the Stay Date, the values are more extreme (cancellation rate of 100% or 0%), and Regression Decision Tree was particularly good in Days Prior period 21-60. Investigating the Tree model, we can see that the top 2 levels both used OTB as splitting variable. In the top level, it already assigned the extreme 0% cancellation rate for 13.5% of total observations. Similarly, Tree model can predict extreme values such as 99% cancellation rate, while Traditional model and Regression never came up with such extremity. Different model performed well in different Days Prior period due to observation variation depending on days prior.

There are some features that proved their importance across models. Cumulative Gross Bookings indicates the demand level for a room and OTB bookings indicates the raw demand level adjusted by cancellations made. Days Prior is also an important factor. It has nonlinear relationship to cancellation rate, as indicated by Regression and Decision Tree model. Product Types is also an important factor. Product type interacted with Days Prior and have distinct cancellation pattern. For example, Government product had increasing cancellation rate as Days Prior approaching days 10 prior to Stay Date. Meanwhile, cancellation behavior for Corporate product manifested as a gradually declining trend line. As Product Type showed distinctive cancellation patterns, we suggest hotels to look deeper into each individual Product Type to find suitable policy for better cancellation control. 

My combined model by linear-regression stacking method was the best-performing model in all Days Prior periods. This result indicated that the meta-regressor generated predictions that resembled cancellation patterns that individual model did not fully capture. 



