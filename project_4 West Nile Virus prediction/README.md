# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) West Nile Virus Prediction

## Members
- Albin Wan
- Daphne Kwok
- Lynette Ng
- Samuel Cheah


## Problem Statement
According to the Centers for Disease Control and Prevention, the West Nile Virus (WNV) is a viral infection transmitted across humans through the bite of an infected mosquito. Mosquitoes first become infected when they feed on birds. 1 in 5 people who become infected with the virus develop a fever along with other symptoms such as body aches, rashes and diarrhea. About 1 in 150 people develop a serious illness that affects the central nervous system.

Kaggle launched a competition with a $40,000 prize money back in 2015 to predict West Nile Virus in mosquitoes across the city of Chicago. Though the competition has already ended, we're working on our own version of model on the same problem set as part of our Machine Learning curriculum with General Assembly. 

Our project aims to answer below problem statements:

1. Predict the occurrence of presence of West Nile Virus given weather, location, testing and spray data
2. Analyze to see if there are main predictors reasons to the West Nile Virus
3. Recommendations on best practices to how to reduce human contraction of the virus

## Executive Summary

Our codebook is split to 3 main notebooks

1. Data Cleaning (`01. Data Cleaning.ipynb`)
2. EDA and Pre-processing (`02. EDA and Pre-processing.ipynb`)
3. Modelling (`03. Modelling.ipynb`)

#### `01. Data Cleaning.ipynb`

Here we include the codes where we did some basic cleaning of datasets. This include patching up `weather.csv` file onto our `train.csv` data set in order for us to proceed with EDA. We also address some data related issues like converting to the right data types as well taking a deeper look into some of the weather features provided.

#### `02. EDA and Pre-processing.ipynb`

We conduct EDA on the data that we clean from earlier notebook. Here we look into relationships of several features like mosquito species, temperature and others against the occurrence of West Nile Virus in order to give us an indicator on which features are more important and where we should do feature engineering on. More importantly, we explored the various correlations as well as cross-correlations on lagged and rolled features on some weather features.

#### `03. Modelling.ipynb`

This notebook contains the codes for our models. We pass our datasets through various models through a GridSearch and analyze our results to obtain the best model. We also provide some analysis on the important features as well as the metrics derived from our model. We also include a section on conclusion and recommendations here. 

Our top performing model was a RandomForestClassfier with ADASYN, with scores of all models summarized below.

| Model                          | Train AUC | Val AUC   | Accuracy  | Recall    |
| ------------------------------ | --------- | --------- | --------- | --------- |
| LogReg (no SMOTE)              | 0.834     | 0.836     | 0.946     | 0         |
| LogReg (with SMOTE)            | 0.820     | 0.819     | 0.748     | 0.754     |
| SGD (with SMOTE)               | 0.810     | 0.818     | 0.753     | 0.774     |
| RandomForest (with SMOTE)      | 0.853     | 0.836     | 0.702     | 0.794     |
| ExtraTrees (with SMOTE)        | 0.84      | 0.822     | 0.691     | 0.815     |
| AdaBoost (with SMOTE)          | 0.853     | 0.833     | 0.795     | 0.669     |
| GBooster (withSMOTE)           | 0.850     | 0.831     | 0.801     | 0.688     |
| XGB (with SMOTE)               | 0.874     | 0.846     | 0.794     | 0.715     |
| LGBM (with SMOTE)              | 0.874     | 0.840     | 0.819     | 0.642     |
| SGD (with ADASYN)              | 0.808     | 0.815     | 0.733     | 0.775     |
| LogReg (with ADASYN)           | 0.817     | 0.816     | 0.752     | 0.741     |
| **RandomForest (with ADASYN)** | **0.857** | **0.838** | **0.691** | **0.808** |
| ExtraTrees (with ADASYN)       | 0.844     | 0.820     | 0.69      | 0.815     |
| XGB (with ADASYN)              | 0.871     | 0.839     | 0.801     | 0.702     |

## Data Dictionary
| Feature Name           | Data Type      | Description                                      |
|------------------------|----------------|--------------------------------------------------|
| Date                   | datetime64[ns] | date that the WNV test is performed              |
| Trap                   | object         | Id of the trap                                   |
| Latitude               | float64        | Latitude returned from GeoCoder                  |
| Longitude              | float64        | Longitude returned from GeoCoder                 |
| Species                | object         | the species of mosquitos                         |
| Block                  | int64          | block number of address                          |
| AddressAccuracy        | int64          | approximate address returned from GeoCoder       |
| NumMosquitos           | int64          | number of mosquitoes caught in this trap         |
| Tmax                   | int64          | maximum daily temperature (F)                    |
| Tmin                   | float64        | minimum daily temperature (F)                    |
| Tavg                   | float64        | average daily temperature (F)                    |
| Depart                 | float64        | departure from normal temperature (F)            |
| DewPoint               | int64          | average dewpoint (F)                             |
| WetBulb                | float64        | average wet bulb (F)                             |
| Sunrise                | int64          | time of Sunrise                                  |
| Sunset                 | int64          | time of Sunset                                   |
| CodeSum                | object         | code of weather phenomena                        |
| PrecipTotal            | float64        | Total Precipitation (inch)                       |
| StnPressure            | float64        | Average Station Pressure                         |
| SeaLevel               | float64        | Average Sea Level Pressure                       |
| ResultSpeed            | float64        | Resultant Wind Speed (mph)                       |
| ResultDir              | int64          | Resultant Wind Direction (degrees)               |
| AvgSpeed               | float64        | Average Wind Speed (mph)                         |
| Heat/Cool              | float64        | Departure from 65 F                              |
| sunset                 | object         | time of Sunrise (datetime format)                |
| sunrise                | object         | time of Sunset (datetime format)                 |
| SunHours               | float64        | Hour difference between Sunset & Sunrise         |
| isRainy                | int64          | 1 = is Rainy and 0 = not Rainy                   |
| Humidity               | float64        | derived from DewPoint and Tavg                   |
| year-mth               | object         | year - month                                     |
| Year                   | int64          | year                                             |
| Month                  | int64          | month                                            |
| Week                   | int64          | week of the year                                 |
| WnvPresent             | int64          | Presence of WNV. 1 = WnvPresent and 0 = Wnv not Present           |
| DewPoint_Roll22Lag1    | float64        | 22-day rolling mean and 1-day lag of DewPoint   |
| WetBulb_Roll16Lag7     | float64        | 16-day rolling mean and 7-day lag of WetBulb    |
| AvgSpeed_Roll22Lag5    | float64        | 22-day rolling mean and 5-day lag of AvgSpeed   |
| Humidity_Roll16Lag1    | float64        | 26-day rolling mean and 1-day lag of Humidity   |
| isRainy_Roll6Lag21     | float64        | 6-day rolling mean and 21-day lag of isRainy    |
| PrecipTotal_Roll1Lag5  | float64        | 1-day rolling mean and 5-day lag of PrecipTotal  |
| ResultSpeed_Roll23Lag5 | float64        | 23-day rolling mean and 5-day lag of ResultSpeed |
| AvgSpeed_Roll22Lag5    | float64        | 22-day rolling mean and 5-day lag of AvgSpeed    |
| Heat/Cool_Roll12Lag12  | float64        | 12-day rolling mean and 12-day lag of Heat/Cool  |
| Tavg_Roll12Lag12       | float64        | 12-day rolling mean and 12-day lag of Tavg       |
| Precip_X_DewPointRL    | float64        | Interaction features                             |
| Precip_X_WetBulbRL     | float64        | Interaction features                             |
| Precip_X_TavgRL        | float64        | Interaction features                             |
| Precip_X_ResultDir     | float64        | Interaction features                             |
| Precip_X_Latitude      | float64        | Interaction features                             |
| Precip_X_Longitude     | float64        | Interaction features                             |


## Conclusion

In conclusion, we found that there are two classes of features that help to predict the prevalence of WNV. The first and obvious one are weather features today that directly affect mosquito activity, and thus mosquito capture rates. Higher temperature days promote mosquito activity, which allows us to catch more of them, while higher wind speeds have the opposite effect of making mosquito traps less effective. The second class of features are weather features lagged and rolled in time to capture the weather conditions present during the previous generation of mosquitos. These conditions affect the activity and survival of the previous generation, which directly impacts their ability to breed and thus pass on WNV through the next generation. Importantly, our prescribed method of using the Cross Correlation Map can be easily used to discover these features further back in time.

## Recommendations

**Explore genetically modified mosquito for Culex breed**
In the United States, the U.S. Environmental Protection Agency (EPA) has authorized use of OX5034 genetically modified Ae. aegypti mosquitoes for release in counties in Florida and Texas. We propose to expand the research to explore other breeds, including for the Culex breed. This technique has proven to be successful in Singapore. Genetically modified mosquitoes carry self-limiting genes that prevents mosquito offspring from surviving to adulthood, hence reducing the target breed of mosquito.

**More active on-the-ground monitoring**
Especially more so during the summer months of July and August, there should be more active ground work to monitor potential breeding areas. Using Singapore as an example, clear guidelines are set to specific areas (e.g. construction sites, schools, residential areas) as to where checks should be done and how frequent it should be done.

**Education**
As much as practical means can be done, most of the responsibility still boil down to individuals to prevent breeding of mosquito. Again using Singapore as an example, there are several means of educating people in terms of mosquito prevention that perhaps Chicago can emulate from. Ranging from short snippets through social media or television broadcast on mosquito prevent techniques to posters being put up in common residential areas, these are all small but powerful ways to nudge people to take ownership of the situation.

To have better prediction power for our model, our recommendations would be to analyze trap data in conjunction with weather data even further back than we were able to. We were limited to a combined lag and roll buffer of 28 days due to data constraints. However, it is possible that due to the exponential breeding abilities of mosquitos, being able to analyze weather conditions 2 or more generations back from the current one could be even more useful in predicting, and hence preventing WNV outbreaks.