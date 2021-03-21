# Project 2 - Reddit Classifier
Building a subreddit classifier
## Introduction
r/options and r/stocks are 2 big subreddits on Reddit devoted to trading discussions related to each type of financial instrument. r/options has a subscriber count of 750k while r/stocks has a subscriber count of 2.5mil. Even though both subreddits are trading focused, we want to examine what features set them apart.

## Problem statement
What are the most representative text features of posts from each subreddit that will allow us to correctly classify them?  This classifier should be able to identify for us the top predictive features for each subreddit, and from there, we hope to additionally answer questions such as "what trading strategies are currently trending within option and stock traders" and "what companies are currently popular with traders".

## Executive summary
This project seeks to build a classifier that is able to differentiate between posts from r/options and r/stocks, two trading subreddits focused on different classes of securities. The classifier should be able to identify what features are important in discriminating between these subreddits and use them to make accurate predictions.

The methodology of our project is as follows:

    1. Scrape data from our 2 subreddits
        - we scrape by top posts, by month. Data was scraped on 10th March 2021.
    2. Data Cleaning
        - ensure no duplicate posts after scraping
        - process text data to make them suitable for EDA and modelling.
        - checking for pseudo duplicates, e.g. megathreads with the same body but different date in title
    3. EDA
        - examine frequency of features
        - examine post length
        - examine post engagement via upvotes
    4. Modeling
        - 2 parametric models
            - Logistic Regression, Multnomial Naive Bayes
        - 4 non-parametric tree models
            - Random Forest, Extra Trees, AdaBoosted trees, GradientBoosted trees
        - 2 Vectorizers
            - CountVectorizer
            - TfidfVectorizer
    5. Evaluation of models
        - compare models based on Accuracy score and ROC AUC score.
        - due to balance of classes, these metrics are very close.

Results show that our Logistic Regression model with TfidfVectorizer produces the best result. It is the least overfit (difference of 5% between train and validation set) and has the highest accuracy (89% after full optimization). Full details of our model testing is discussed in our 3rd notebook.

We found that top feature predictors for r/options are more technical in nature and unique to option trading strategies and options in general. Examples include terms like `call`, `put`, `premium`, `credit spread` and such. Top feature predictors for r/stocks show an emphasis on fundamental research on companies or the broader market. Examples include terms like `invest`, `revenue`, `market`, and `company`.

Additionally, we examined the misclassified posts and noticed that our model produces many more false negatives than positives. After examining common features of posts that were misclassified, we added in additional stop words and increased our model's performance by 1%.

## Recommendations
Our first recommendation to users wishing to improve on our model would be to continually train it on a larger corpus of text. Our data was gathered from the top 1000 post from each subreddit in a month. One could feasibly scrape a new set of 1000 posts every month from each subreddit, adding to the amount of training data available for our model to learn from. This will hopefully allow our model to learn how to identify especially those r/options posts that read like r/stocks posts. There is a caveat here that we discuss in limitations section below.

Our second recommendation to users wishing to take our model one step further would be to explore the use of named entity recognition through libraries such as spaCy. The use of named entity recognition could allow one to focus on identifying trending companies within a subreddit as a means of gauging retail sentiment. This is of incredible use to anyone who is keen on using retail sentiment to forecast price movements and trading volume. In addition, if one is able to extend named entity recognition to identify unique stock/option trading strategy names, one would be able to get a sense of popular, well-used strategies. This could be of use to a beginning investor who would like to know what strategies many people are using, so that he can focus on learning them. 
