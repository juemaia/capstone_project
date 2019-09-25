# Introduction and Objective

Drivvo is a mobile app to record and keep track of vehicle expenses and keep on top of regular maintenance. The app has more than 2 million registered vehicles and users from more than 180 countries. Currently the app's main function is to create reports on the vehicle services and expenses based on the users inputs. 

The main objective of this project was to make the app more consultative, trying to predict when the vehicle would need its next service.


# Methods and Conclusion

## Getting the data

The Drivvo database is stored in a PostgreSQL system with more than 30 tables. The first step of this project was to extract the data by identifying which columns from all the tables could be used for predicting a vehicle service.
I used SQL commands to join the tables and extract the data needed. I extracted information regarding country, language, currency, vehicle services and vehicle attributes like brand, model, type, fuel tank volume and others. Because Drivvo’s dataset is very big, I selected the country with largest number of users, which is Brazil. The data was saved into a csv file.

## EDA

The next step was to perform exploratory data analysis and cleaning using python in a jupyter notebook. I started by subsetting the data to only keep oil change, the most frequent service. 

The initial idea was to predict when the next oil change is supposed to happen.  Because some of the data were inputted by users, there were no patterns, for example, same vehicle model names differed greatly between users, also there were some misspellings, typos and large number of null values. This leaded the first attemptive to more than 12k different vehicle models and a negative R squared score on a linear regression model.

My second approach was to work on the data cleaning and try to extract as much information as I thought would be useful for the prediction from the users inputs. I used regex, dictionaries, lambda, masks and other pandas and numpy commands for the data cleaning.


## Defining the target

The main goal of my project was to predict when the next oil change would occur. Initially I thought about predicting dates by running a time series model, but it would not be accurate since what influences most on a vehicle service, in this case, oil change, is how much the vehicle is being used rather than when was the last service in terms of date. 

Considering  that users would input the odometer reader mileage (in kilometres or miles) at the moment of the service,  I decided to use the difference in that parameter between services, so it would tell about how much a vehicle is being used until the next need for oil change. Because most of the vehicles have multiple entries for the same service, they could potentially autocorrelate on a regression model, therefore I just kept one entry per vehicle id, using the mean difference on odometer reading mileage between services for each vehicle id.

The target variable had a skewed distribution, so I manually dropped the outliers, keeping just values between percentile 5 to 95. 

## Preprocessing 

As predictors I used the variables 'odometer', 'brand', 'vehicle_type', 'fuel', ‘fuel_volume’ and ‘year’.
I dummyfied the categorical variables (brand, vehicle_type, fuel), standardised the predictors and splitted the data into train and test sets.


## Modelling

As my target is a continuous variable, I used different regression models for the predictions, using cross validation and grid searching for the best parameters.

## Results and Conclusions

After comparing 8 different regression models on their cross validated and test R squared scores, the best result I got was from the random forest regressor model. I also observed that all the models were good at generalising since the test and cross validated scores did not differ greatly in any of the models.
The random forest regressor model showed that around 59% of the variation on the target is explained by the independent variables. Although an R squared score of 0.59 is not necessarily good,  it is accurate to say that the model performed better than the baseline that, in a regression scenario, is the mean of the target variable. Also, since the score is positive, it is right to assume that the Residual Sum of Squares (RSS) is smaller than the Total Sum of Squares, which is another indicator of a good model.
Because the R squared is a measure that doesn’t convey the reliability of the model, I also checked for the residuals distribution that showed a gaussian curve kind of distribution. Normally distributed residuals indicates that the regression is modelling the linear relationship appropriately and that the assumptions of the linear regression are probably being met.

Those reasons, added to the fact that I don’t need to know the weight of my variables for the app’s predictions and also considering that the app aims to make a suggestion rather then being precise, the Random Forest regressor seems like a good model of choice.

When looking at the model feature importance, that shows which features are more influential on splitting the tree nodes, it is possible to see that the tank fuel volume, year of the vehicle and odometer reader mileage are the most important features for that model. Interestingly, those are the features with highest weights for the linear regression with no regularisation and also for linear regression with ridge and lasso penalties. This could be something to investigate further in order to identify vehicle’s performance.


# Next Steps

As a future perspective, could be interesting to investigate further the role of the features on the vehicle's performance and how it would also affect its expenses.

Furthermore, the idea is to expand the model for other countries where Drivvo has users and to create similar models for different services.

One of the main findings of this project was identifying the difficulties that the users have while inputting data. For that reason, improving the user interaction inside the app and, therefore, obtaining more useful data is a priority for the future.
