# summerProject
# Data Cleaning 
3652 records had a state of undefined
  If the goal was met or exceeded state was set to 'successful' if not it was set to 'failed'

3082 records had '0' for backers, yet money was pledged.  Imputation was attempted using the 'Mice' package in R, but after running for 24 hours only about 1800 values were calculated.
Median was used to calculate instead.  Of the 3082 records, 1759 had a state of 'successful' and 1326 had a state of 'failed'.  The Median backers were determined for successful projects with pledged amounts between 1 - 10000 ( 11 ) and 10000 - 20000 ( 14 ) since this was the range for the values we were imputing.  There was one project with 0 backers and a pledged dollar amount around 2 million.  The median was determined for successful projects between 2 - 3  million ( 1296 ).  The same was repeated for the failed records although the range of missing backer data was only between 1 - 8000, so the median was determined between  1 - 2000 ( 9 ) and 2000 - 8000 ( 64 ) 

Feature Engineering

duration : launched - deadline
usd_short : usd_goal_real - usd_pledged_real
believer_ratio : backers / usd_goal  * 1000
hope_ratio : usd_pledged_real / usd_goal * 100
dollars_needed_per_day : usd_goal_real / duration
hope_slope : pledged_dollars_day / dollars_needed_per_day 
backers_per_day : backers / duration
launched_year: the year project was launched

Because we had so many features there was a lot of correlation in the data set, so models were run removing highly correlated predictors
There were a lot of issues becuase of the size of our data set when trying to run repeated 10 fold cv.  It was pretty much impossible unless we let our programs run for 24 + hours.

Models attempted:

KNN: Attempted to use the 'caret' train function on all non-correlated predictors from 2012 - 2017.  I used repeated 10 fold cv ( repeat of 10 times ) this ran for over 24 ours so I cancelled it.  I ran the KNN again on a random sample of only 10000 predictors from our training set and got an optimum k of 5 so reran on the entire training set and then tested 

           testing_y
knn_pred_y   failed successful
  failed      54615          1
  successful     44      35470

Accuracy: 0.99
Specificity: 0.99
Sensitivity: 0.99

This is expected seeing as our data has the answers in it.  Obviously if the hope_slope is greater than 1 then the project is successful, same thing for the hope_ratio; if it's greater than 1 then the project will be successful

We need data that exists already at the beginning of the project in order to predict.
Or we need snapshots of data during the time of the project; i.e. how much was raised after 1 week, 2weeks, etc.... in order to actually run a model on current projects to try and predict

the only data we have that exists at the beginning of the project is Category, duration, and goal

Ran Knn on 2012 - 2017 data ( same as above ) but only using main_category, goal, and duration 

predictedK   failed successful
  failed      47532      34162
  successful      0          0
  
Accuracy: 0.58
Sensitivity: 0.00
Specificity: 0.58












