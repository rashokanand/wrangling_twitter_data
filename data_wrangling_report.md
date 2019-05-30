# Data Wrangling report

This report deals with a walkthrough of the process of gathering, cleaning and putting to order of some twitter data. 'WeRateDogs' is a famous twitter account, that tweets their ratings for dogs. It collects photos of dogs from various sources such as other twitter users and followers, posts the picture along with a humorous statement and a rating. Our data consists of all the tweets of this account that they have posted ever (over 5000 of them).

The Udacity team received the dataset from 'WeRateDogs' and then have provided to us after a little processing. Only keeping those tweets that contain ratings. They already have extracted some details from the text of the tweet such as the dog name, dog rating numerator and denominator and the dog stage. Hence this is named twitter_archive_enhanced. 

In addition to this, Udacity also have given an image predictions dataset. This consists a prediction of the breed of dog from the image posted using an image classification algorithm. The data consists of 3 predictions for each image and the confidence level of each prediction.

There is some missing data in the twitter archive dataset though. Some of the notable omissions are favorite counts and retweet counts. The process of obtaining of these indicators and the overall cleaning for tidyness and quality issues *is* the project. This is further followed by a report on a few insights and visualizations created using the cleaned data.

## The Gather step

The twitter_archive_enhanced dataset was provided as a csv, which I imported using the pandas.read_csv method. And the same goes for the image predictions dataset as well. The dataset was a tsv - Tab separated values - file, so '\t' was passed to the 'sep' argument in the read_csv method. The downloading part of the image predictions file was done programmatically as instructed in the project requirements. The link was provided, which was queried using the requests library's get function.

Using Tweepy - an easy to use python library to access the twitter API - each twitter id is queried for all the tweet related data. Using Tweepy was fairly straightforward, however obtaining the API 'key(s)' - that are needed to access the API - was not. It entails creating a developer account at [developer.twitter.com](developer.twitter.com), and then creating an app. It asks for several details related to usage and data privacy if the app is developed and used.

Each twitter id's queried data comes as a json formatted text string. I used the json.dump(s) method to store the so received dataset. All the so downloaded text data was dumped using the json.dump method to tweet-json.txt.  

Then using pandas to import and create a pandas dataframe of the so downloaded data. I decided to only keep the favorite and retweet counts for each tweet id. More on this later, during the assess and clean steps.

## The Assess step

The assessment for quality and tidiness issues was done using a combination of the pandas methods of head, tail, info and value_counts.

The further tweet related data that was downloaded programmatically was thrown away after joining the required retweet and favorite columns with the twitter_archive dataset. Hence now I am left with only the twitter_archive_clean_df and the image_pred_df. Hence I assess and clean these datasets only.

In total 2 tidiness issues and 11 quality issues were identified and cleaned for the two datasets.