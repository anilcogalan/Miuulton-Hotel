# HOTEL BOOKING CHURN PREDICTION

![image](https://github.com/anilcogalan/Miuulton-Hotel/assets/61653147/cd75627f-5bd2-4285-919b-b2c0e545bdeb)

The hotel industry has a high degree of competition in today's market. Competition for customer retention is high for any hotel. The ability to predict customers who are most likely to leave can reduce the cost of hotels and help make proactive decisions. The aim of the project is to anticipate potential customers who may cancel their reservations and to prevent cancellations by offering an incentive or discount.

## Dataset

The dataset used in the project was taken from Kaggle named "Hotel Reservation Dataset". It has 36,275 observations and 18 features related to hotel reservations.
Attributes are a mix of categorical and numerical data. The target variable is "is_canceled", indicating whether the reservation has been cancelled.

| Variable Name                        | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| no_of_adults                         | Number of adults in the reservation                          |
| no_of_children                       | Number of children in the reservation                        |
| no_of_weekend_nights                 | Number of nights stayed during weekends                       |
| no_of_week_nights                    | Number of nights stayed during weekdays                       |
| required_car_parking_space           | Indicator of whether car parking space is required            |
| lead_time                            | Number of days between booking and arrival date               |
| arrival_year                         | Year of arrival                                              |
| arrival_month                        | Month of arrival                                             |
| arrival_date                         | Date of arrival                                              |
| repeated_guest                       | Indicator of whether the guest is a repeated guest            |
| no_of_previous_cancellations         | Number of previous canceled bookings by the guest             |
| no_of_previous_bookings_not_canceled | Number of previous bookings by the guest that were not canceled |
| avg_price_per_room                   | Average price per room                                        |
| no_of_special_requests               | Number of special requests made by the guest                  |
| booking_status                       | Indicator of whether the booking is confirmed (1) or unconfirmed (0) |



### EDA

* An imbalance has been observed in the data set:
	- 67% 1 so not_canceled(not cancelled)
	- 33% is 0 so canceled

* Average early reserve dates of canceled reservations are **139 days**
determined as **59 non-cancellable** days.


* With the increase in the number of special requests, the probability of reservation cancellation has decreased. **There is a negative low correlation**.

### Feature Engineering

* no_of_week_nights --> total number of overnight stays for customers arriving on weekdays

* no_of_week_nights_category --> we did a kind of rare analysis [The number of reserves over 4 days was low. It has been seen and it has been decided to perform rare encoding.]

* no_of_children --> It has been seen that the number of children more than 2 is only 2 rooms old and these rooms are suppressed.

* It has been seen that the number of adults larger than 3 is less in the rooms, and this number of people has been suppressed to 3 in order to avoid unnecessary months and less necessary columns in the endcoding process.

* no_of_nights --> total number of nights(weekdays+weekends)

* Total_price was obtained by multiplying the average prices of the rooms with the number of nights we derived.

* 2 new variables are derived by multiplying the rooms rented on weekdays and weekends by the average room prices.

* Reserve. The seasons were formed over the months.

* From room_type_reserved :
	Since room_type_1 is very close to 0, it is assigned to 0 class and the remaining room types 1,2,3,.. are changed from cheap to expensive and assigned to the variable named 'roomy_type_categorized'.

* The general price distribution of room types is as follows:

| Room Type | Avg. Price per Room |
|-----------|-------------------:|
| 1         |             95.919 |
| 2         |             87.849 |
| 3         |             73.679 |
| 4         |            125.287 |
| 5         |            123.734 |
| 6         |            182.213 |
| 7         |            155.198 |

Note: Based on the sales strategies, considering that the 'Up-Sell' technique is applied in the service of the hotel, it is predicted that type_4 offers a feature with a difference of 2 units and is therefore more preferred.

5.Modeling

The approach adopted for modeling is to construct multiple classification models and compare their performance. The algorithms used are LR,KNN,SVC,CART,RF,Adaboost,GBM,XGBoost,LightGBM. Hyperparameter tuning is done to optimize the performance of the models. Models are evaluated using appropriate metrics such as accuracy, recall, precision, and F1 score. The best model is selected based on the highest **F1 score because of unbalanced data**.

6.Results and Conclusion

The project concludes that it is possible to predict customers who are most likely to cancel their reservations. **The LGBM model performs best with an F1 score of ~0.93**. Hotels are encouraged to use this model to predict potential cancellations and offer an incentive or discount to retain customers. The limitations of the analysis include the need for more data on customer behavior and preferences. Future work includes collecting more data and conducting an in-depth analysis to determine the reasons for the cancellations.

7.References

* Hotel Booking Dataset: https://www.kaggle.com/mojtaba142/hotel-booking 
* H. A. Abbasi and A. Hossain, "Churn Prediction in Hotel Industry Using Machine Learning," 2019 IEEE International Conference on Smart Systems and Technologies (SST), 2019, pp. 1-6, doi: 10.1109/SST.2019.8724088.
