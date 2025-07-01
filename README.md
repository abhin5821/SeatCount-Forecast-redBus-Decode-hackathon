# **SeatCount Forecast: redBus Decode Hackathon 2025**
Source : [redBus Decode](https://www.analyticsvidhya.com/datahack/contest/redbus-data-decode-hackathon-2025)

## Problem Statement
Predict the final seatcount for the given date of journey 15 days prior the departure.
The given dataset consists of the follwing-
- Seats booked: Historical demand data.
- Date of journey: The actual travel date.
- Date of issue: The date when the ticket was booked.
- Search data: The number of users searching for a particular journey date on a given booking date.



## Solution
### Rank: 106/694 teams
The proposed solution for demand forecasting of seat count is modelled using a CatBoost regressor, which yielded an RMSE score of 651.71 for the test dataset.

The solution commences with an analysis of the provided datasets. Based on the observations, weekly seasonality is evident. Additionally, there is a discernible increase in seat counts at specific dates, particularly at the commencement and conclusion of the year, suggesting the presence of special days or holidays.

The feature engineering process involves the following steps:
- Extracting essential datetime features from the ‘doj’ column, including date_of_month, week_of_year, month_of_year, day_of_week, start_and_end_of_year.
- Extracting holiday data from an external holiday dataset (https://www.officeholidays.com) and concatenating it with our data as two indicators: National and Regional holidays.
- Creating lag features (1 and 7) based on daily pickup 1 and 7 days before booking-on-hand (15 days).
- Generating Fourier features (sine and cosine).

The aforementioned engineered features are appended as columns based on the route_key (date, srcid, destid).
Prior to initiating the training phase, only records where the date of departure is 15 are considered, as the objective is to predict 15 days in advance. 

During the training phase, several regressors and approaches have been incorporated, including CatBoost, XGBoost, LightGBM, and RandomForestRegressor. Among these models, the CatBoost model with basic parameters demonstrated superior performance for the test dataset, achieving an RMSE score of 651.71.

Overall, this hackathon provided a comprehensive exploration of the concept of forecasting and the various approaches employed in this field.

## References
1. https://www.kaggle.com/code/ryanholbrook/linear-regression-with-time-series
2. https://link.springer.com/article/10.1057/s41272-023-00421-1
3. https://medium.com/@chenycy/predict-hotel-demands-leveraging-time-series-forecasting-techniques-62e25606f273
4. https://dspace.mit.edu/bitstream/handle/1721.1/68058/FTL_R_1987_01.pdf;sequence=1
5. https://www.trendytechjournals.com/ijtret/volume8/issue4-6.pdf
6. http://arxiv.org/pdf/2401.03397
7. https://www.mosaicatm.com/wp-content/uploads/2021/04/matm-revamping-airline-demand-forecasting-wp.pdf










