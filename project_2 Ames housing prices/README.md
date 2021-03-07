# Project 2 - Ames Housing Prices
Predicting housing prices with linear regression models
## Introduction
The housing market is a nebulous entity to the majority of people who don't regularly interact with it. It can sometimes seem very arbitrary how prices are determined. This makes it especially hard for first time buyers or sellers to know where or how to start transacting in the market.

## Problem statement
Can we use linear regression to predict housing prices based on a given set of predictor variables? The model we build in this project will help to aid all market participants, not just buyers, to make informed decisions on buying, selling, or even upgrading their houses, to optimize their value. We use RMSE as our error metric when evaluating our models.

## Executive summary
This project seeks to understand the relationship of house prices in Ames, Iowa, with a set of 80 different housing related variables. Examples of such variables include the total above ground living area, the neighborhood the property is located in, and the year the property was built. We seek to build a regression model that can use a number of these variables to accurately predict future house prices when used on new, unseen data.

The methodology of this project is straightforward:

    1. Clean our data
        - including preparing data for exploratory data analysis by performing the appropriate transformations such as splitting data in train and validation sets.
    2. Perform our EDA
        - we will employ the use of summary statistics and visualizations such as scatterplots, heatmaps, and boxplots.
    3. Preprocess our data
    4. Model our data
        - we employ multiple linear regression, ridge, lasso, and elasticnet models.
    5. Evaluate models.
        - the metric used shall be Root Mean Squared Error (RMSE).
Results show that the optimal model to use is the **Lasso regression model with 30 predictor variables**. The model display a good balance between prediction power and generalizability without making our model overly complex, as the difference in performance between our training and validation sets is a reasonable RMSE of 1000 or so. The exact details of this model's implementation are included in our model evaluation.

## Recommendations

We find that the top predictors that explain housing prices are the neighborhood the property is located in, the various size dimensions of the property, as well as variables detailing the quality of various aspects of the property.

**For buyers** for whom location is not a big issue, we recommend looking at properties located outside neighborhoods such as Stone Brook and Northridge Heights. You would be able to get house of significantly better quality and size for the same price as a property in one of those expensive neighborhoods. **For sellers** looking to increase the value of their house, we recommend either expanding the liveable area of their property, or to invest in upgrading the quality and finish of their house. **For developers** looking to build their next profitable project, we recommend developing them within neighborhoods like Stone Brook and Northridge Heights.

Recommendations for future action include the **exploration of interaction effects** between our existing variables and **building individual regression models for each neighborhood** to account for the difference in importance of various predictors between neighborhoods.

Some limitations of this project include being unable to comprehensively explore all possible interaction effects of our predictors, as that requires more time and computing resources. We also chose to favor a lower complexity model here, so it is like that our model could be finetuned further if we are willing to accept an increase in model complexity. We would also benefit from having more data as a whole, and having that data be more complete as well.

## Data dictionary
The data dictionary for the Ames housing dataset can be found [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).
