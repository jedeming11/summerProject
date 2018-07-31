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








