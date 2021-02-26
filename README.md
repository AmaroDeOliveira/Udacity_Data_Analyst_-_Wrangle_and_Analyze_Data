# Wrangle and Analyze Data - WeRateDogs (@dog_rates) Twitter Account
## by Lucas Amaro de Oliveira

Project to Udacity in partial fulfillment of the requirements for the Danalyst Nanodegree.

## Table of Contents

* [Introduction](#Introduction)
* [Data Wrangling](#Data-Wrangling)
* [Summary](#Summary)

## Introduction

We love dogs, but same times WeRateDogs!!!!!!! One Twitter account is completely dedicated to that.
The most unique characteristic of the popular WeRateDogs (@dog_rates) account is its rating scheme where dogs are rated in a 0 to 10 scale. In this particular scale, the dogs usually achieve 11, 12, 13… because "they're good dogs Brent." Over time the ratings had growth as the populate of the account. Since July 2016 the dogs that are rated below 10 are very few (and probably a mistake of the text interpreter).

## Data Wrangling

In this project, the data were gathered from three different sources. The first CSV file contains the bulk data from tweets of the account WeRateDogs (@dog_rates). The texts were pre-processed and saved in the 'twitter-archive-enhanced.csv' CSV file. A second file contains the results of image analysis saved in a TSV file named 'image-predictions.tsv'. the last source is the current (2021-Feb-04) status from the describer tweets, which were gathered using the ‘tweepy’ API. From the status was used ‘favorite_count’ and ‘retweet_count’ information. These three data were stored in a three separated Pandas DataFrames, ‘twitter_archive_df’, ‘image_predictions_df’, and ‘tweet_statuses_df’, respectively.
In the assessment part of this project the following issues were found:
Regarding Quality
Enhanced Twitter Archive table
-	‘timestamp’ and ‘retweeted_status_timestamp’ columns type are string, not datetime type.
-	‘in_reply_to_status_id’, ‘in_reply_to_user_id’, ‘retweeted_status_id’, and ‘retweeted_status_user_id’ are are of type float and should be of type string.
-	Nulls represented by the string 'None' in 'name', ‘doggo’, ‘floofer’, ‘pupper’, and ‘puppo’ columns.
-	Strange rating_denominator values (ie. 0, 2, 7, 11, 15...). Same for rating_numerator.
-	Unoriginal ratings (retweets).
-	Unnecessary columns
Image Predictions table
-	Missing information: ‘image_predictions_df’ has 2075 rows and ‘twitter_archive_df’ has 2356 rows ***(can't clean)***
-	Same tweets are not dogs (according to the prediction).
-	Unnecessary columns
Tweet Stuatus Counts table
-	Missing information: ‘tweet_statuses_df’ has 2308 rows and ‘twitter_archive_df’ has 2356 rows ***(can't clean)***
-	Inconsistent ‘tweet_id’ column datatype
Regarding Tidiness
-	 ‘pupper’, ‘puppo’, ‘doggo’, and ‘floofer’ should be a single column of type category
-	All tables forms a single observational unit. Therefore, they can be brought together as single data frame.

To clean the data, the three DataFrames were copied, so that the originals are kept as a reference.
The unnecessaries columns were deleted using the Pandas’ ‘drop’ method. Pupper, puppo, and doggo columns were collapsed int a new ‘age’ column. The columns with the wrong datatype were change using Pandas’ ‘astype’ method and ‘to_datetime’ function. The DataFrame were merged using Pandas’ ‘merge’ function. And the wrong cell's content (Nullrepresenteded by ‘None’) were corrected using Pandas’ ‘replaced’ method.

## Summary

- The data is very dispersed, the range is quite big and the outliers are many. 'favorite count' and 'retweet_count' are very skewed to the right: some tweets are very popular, but most don't.

- The dog rates that exceed the limit of 10 are the most favourited and retweeted. However, if it is because of the cuteness of the dog or the uniqueness of the rating scheme is yet to be discovered. The tweet favourite and retweet counts look very similar, maybe correlated.

- Over time the ratings had growth (inflation).

- Puppers are more common than puppos, doggos, and floofers combined. Puppers also had a lower rate and much lower popularity than puppos, doggos, floofers. Despite of puppers natural cuteness they are not as much as popular as the puppos and doggos. One could speculate that this is becouse of these tweets are more common.

- The number of elapsed days; the rate; the puppo and doggo stage appears to have a strong positive influence on the favourite count and the retweet count. The p-value for pupper, floofer and multiple_stages are very high. Therefore these features should not be considered.