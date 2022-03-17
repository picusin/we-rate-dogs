# WeRateDogs wrangling and analysis
## by Miguel Orellana

This was the fourth project of Udacity's Data Analyst Nanodegree, completed at the end of the Data Wrangling section.

WeRateDogs (@dog_rates) is a Twitter account that rates people's dogs with a humorous comment about the dog. The goal of this project is to wrangle their Twitter archive and extract some visualizations from it.

## Dataset

There are three different datesets in this project:

### 1. WeRateDogs Twitter Archive:
This first dataset is the main one and contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017. This archive has been previously enhanced by Udacity, extracting rating, dog name and dog stage from the Tweet text. It has also been filtered to contain only tweets with ratings.

### 2. Twitter API:
Additional information for each tweet is obtained by querying Twitter's API. This process is included in the project's notebook although Twitter API keys are hidden.

### 3. Image predictions:
The last dataset provided by Udacity contains image predictions obtained through a neural network that can classify breeds of dogs. The table includes the top three predictions alongside each tweet ID and URL.


## Wrangling Summary

This project illustrates the data wrangling process of data analysis, from gathering the data to visualizing it and extracting insights. The main goal is to understand and go through the three steps for getting the data ready: data gathering, assessment and cleaning.

### 1. Data Gathering:
In this case the data is collected from 3 different sources and using 3 different methods:

WeRateDogs twitter archive, provided as a .csv file.
Tweet image predictions, provided as a .tsv file.
Additional Twitter information obtained with Tweepy.
The third one was the most complex to obtain, as it involved using a tool that was unknown to me until now, and I had to do some research to understand how Tweepy works.

### 2. Data Assessment:
The data assessment, both visual and programmatic, showed that most of the issues were located in the first dataset, the WeRateDogs twitter archive. The other two dataframes had less information than the first one and were therefore less complex, so they presented less quality or tidiness problems.

For the visual assessment I used Excel in addition to Jupyter Notebooks, as it allowed me to view the entire dataset. Many of the issues detected were spotted by this visual assessment. I then used programmatic assessment to find other issues and also confirm and evaluate the ones that had been identified visually.

Here's the complete list of issues:

#### Quality issues

df1: Several dogs have the name "a" which seems to not be a proper name for a dog.

df1: A few dogs have "None" as a name, which seems to indicate a correct name is missing.

df1: Several dogs have a very high rating_numerator (+100), which seem to be out of the actual scoring range.

df1: Some dogs have two "stages".

df1: Some dogs have a rating_denominator different than 10.

df3: Many tweets have a favorite_count of 0 while having a high number of retweets, which seems unusual.

df1: timestamp and retweeted_status_timestamp are strings when they should be datetime.

df1: Some id columns are float type and some are integers.

df1: Missing values for expanded_urls

df2: Missing images for some tweets. Only 2075 rows in df2, whereas df1 has 2356 rows.

df2: Dog breeds using uppercase and lowercase strings.

df2: Non dog-breed predictions could be replaced by a single value to group all the wrong predictions.

df1: Some tweets aren't original. The columns in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id and retweeted_status_user_id have values only for reply tweets and retweets, so these columns could be used to quickly identify non-original tweets.

#### Tidiness issues
df1: The dog "stage" is separated into four different columns, each of them for a different category, while they could be combined in a single column.

All three dataframes contain related information and could be merged into a single dataframe.

### 3. Data Cleaning:
The Data Cleaning process was the longest part of the project. It started with completeness issues, followed by tidiness and quality issues.

I realized on this step how important iteration is in data wrangling. In some cases, multiple issues got solved at the same time. For instance, some quality issues were resolved by cleaning tidiness issues, as some rows or columns (containing both issues) were removed. In other cases, I decided to solve two related issues at the same time, in order to save time. I also had to change my mind about the order on which to clean the issues a few times, to make the process a bit more comprehensive for myself.

It has been overall a good practice for understanding the entire wrangle process, with the focus being on the cleaning part.

## Key Insights

### Dog Score distribution:

By looking at the rating distribution without outliers (rating_numerator variable), that shows a left sckewed histogram, we can see that the scores given to dogs tend to be on the higher end of the range. The average and the median are very close, at around 11. We could also observe that the majority of dogs had a rating between 10 and 13, and the extreme values were the least used.

![Score distribution](/images/fig01.jpg)

### Dog Stage distribution:

I also wanted to know if the dog stage variable had any impact on the ratings that dogs received. When looking at the 4 different stages separately, we saw that doggo, floofer and puppo got a higher average and median scores than the rest of the dogs (more than 1 point in some cases). However, pupper had a score similar to the dogs without stage. When separating into 2 categories (with and without stage), we saw the values got very similar to each other, which may be explained by the fact that most dogs with a stage assigned were puppers (see visualization below), the ones with a lower score average.

![Score distribution](/images/fig02.jpg)

### Correlation between rating and retweets:

I finally wanted to know if better rated dogs also had more retweets and likes from the WeRateDogs followers, as could be expected. However, the correlation between the score given by WeRateDogs and the favorite_count/retweet_count from their followers very high (0.02 for both), which indicates that dogs with higher scores aren't necessarily the ones that the public likes the most.

![Score distribution](/images/fig03.jpg)
