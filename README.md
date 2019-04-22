
# Utilizing NLP to Classify Political Subreddits (Democrats vs Republicans)
## Contents
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusion and Recommendations](#Conclusion-and-Recommendations)

### Problem Statement

What patterns exist in online text that we can extract, analyze and use to refine online business models? I will be utilizing Natural Language Processing (NLP) to determine whether the author would be closer aligned to the Democratic or Conservative parties, by analyzing /r/Democrats and /r/Conservative on Reddit. 
The goal will be to build and test an assortment of classification models that can predict whether the author is more likely to hold conservative or liberal views, so that we can advise an online advertiser which ads to run for which audiences.


### Executive Summary
Part 1 of this project focuses on the data gathering, wrangling, cleaning and processing from "Natural Language" to something that computers can interpret and model, specifically numerical values. 

The source of our data is one of the current most popular websites for conversations, discussions and arguments on the internet, none other than www.Reddit.com. Home to over 26 Million monthly users, 850,000 subreddits and 18 billion monthly pageviews, Reddit is one of the premier locations on the internet for distribution, manipulation and consumption of data. What better way for us to test a model's ability to classify input into discrete classes than the hotbed of online discussion itself?

In our efforts to classify the text, we will be combining the text from the title as well as the body of the post in order to maximize our analytical process' capacity. This will provide a larger corpus for each post, which will result in a largely and hopefully more robust corpora to train our algorithm. In comparing the subreddits by the numbers, r/Democrats has less subscribers with 91k as compared to /r/Conservative’s 205k, but how do their word usages stack up?

We begin by utilizing the Reddit API to scrape the information from two politically themed subreddits: /r/Democrats and /r/Republicans. In total, we will attempt to pull 1000 posts per subreddit for a total of 2000, but understand that we may fall short due to duplicates or issues with the API's limits. 

After reading in the data, we ensure there are no duplicate posts, we utilize the Pandas library to convert all title and post text dictionaries into dataframes where the text and subreddit location are included, but the subreddit itself is binarized in order to make it feasible for our model to understand. 

Our dataset is then split up into train and test partitions before being fed into a series of models in order to determine the most apt model for our use. The vectorizers that we will employ in order to tokenize the words and additionally clean the text are: CountVectorizer as well as TF-IDF Vectorizer. Although similar to CountVectorizer, TF-IDF is being utilized due to the vectorizer's purpose in controlling the frequency of terms across documents and datasets alike, introducing penalties for reoccuring words. This will help us in our attempts to understand the online text that we have scraped.

For the model selection, we have many at our disposal but will be utilizing the following: LogisticRegression, MultinomialNaiveBayes, RandomForest and finally AdaBoost. These are models that are adept at classification problems in which we are seeking to understand if something is one of two possibilities, with success being measured in Accuracy.

Before getting to the modeling however, we will save the dataframe to a .csv file, in order to lower the potential for needing to rescrape the data and subsequently starting over on the analytical process. Part 2 of this Notebook will pick up from where the end of Part 1 leaves off, with importing the newly formed .csv files and proceeding as planned.

### Conclusion and Recommendations

All of our models performed better than the baseline accuracy metric of ~55%, and although almost all of the models displayed different varying degrees of bias, variance and overfitting, the optimal models were LogisticRegression with CountVectorizer. These were determined not only in terms of overall raw accuracy, but in terms of variance and goodness of fit. 

In recommending this model to be used for the purpose of advertising companies who wish to target potential clients, it is important to weigh the pros and cons of 82.25% accuracy as offered by the Logistic Regression version of our model. This would mean that although 4 out of 5 recipients would be accurate, there would still exist a consistent 1 out of 5 audience that was not actually in the class described by our model. 

Additional features could also serve to improve the accuracy of our model, three ideas for that in future iterations include:

1. Fixing typos or other spelling errors that may have impacted our model's ability to interpret text
      
2. Incorporating a sentiment analysis aspect, which would involve creating two bags of words in which  we define positive and negative sentiment words, then filter and weight them accordingly.
      
3. Incorporate a loudness aspect, in which we would look at the prevalence of capital letters in sequence. Although our preprocessing transforms all text to lowercase, there is an argument to be made for the inclusion of series of uppercase text as it usually conveys intense emotion. 