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

## Recommendations
Recommendations for future improvement of our classifier include scraping more posts every month to increase the corpus we can train our model on. The exploration of named entity recognition and sentiment analysis is also recommended for users wishing to use our classifier to identify what companies are most frequently discussed on a given subreddit, as well as the valence of the discussion surrounding these companies.

A limitation of our current model is that the content of discussion on these subreddits can vary over time, as market trends are constantly evolving. As such, topics that in vogue currently may fade into obscurity 6 months from now, which will throw off the performance of our classifier. Hence, this classifier will need to constantly be retrained at an appropriate time interval in order to maintain its performance.
