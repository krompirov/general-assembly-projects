# Project 1: SAT & ACT analysis (2017/18)
***
## Introduction
The SAT and ACT are 2 popular standardized tests used in the USA for college admissions. They each have their own subtests and grading scheme, which means comparing the results of these 2 tests is not straightforward. In general, students opt to take one test over the other, and this is largely down to state and regional trends.

In this notebook we explore trends in participation rates and test scores for the SAT and ACT for 2017 and 2018. Of especial interest to us are participation rates for the SAT. Together with other additional research, we will discuss factors which affect participation rates, and put forward recommendations to increase participation in the SAT.

***
## Data exploration
#### Importing and cleaning
We start by ensuring our data is cleaned and correctly typed. Erroneous values are fixed.
#### Exploratory Data Analysis
We take an initial look at our data to identify preliminary trends and interesting observations.
#### Visualizations
We employ histograms, boxplots, and regression plots to explore distributions and trends between variables.
#### Descriptive and Inferential Statistics
Together with our visualizations, we describe basic summary statistics for our variables, and discuss their suitability for further inference.
#### Additional research
Armed with our analysis and observations, we further investigate factors which affect our variable of interest, SAT participation rates.

***
## Summary of findings and additional research
Participation rates tend to be biased towards full participation or low participation, with values around 50% being less common. This is because in states that have chosen to forgo their own standardized testing in favor of the SAT or ACT, they will often mandate one of these tests across the state but not both. There are many more states that have mandated the ACT than the SAT, and this shows up in our analysis. The median rate for the ACT in 2018 is 66% while that for the SAT is 52%.

While educational policy regarding the use of the SAT/ACT is a big factor in determining participation rates, two other factors have come up in our research.

The first is the level of financial support given by the state. States which make a test free for their students to take tend to see high levels of participation. Often, states which mandate the use of these tests will also sponsor the costs involved.

The second factor is the logistical accessibility of taking these tests. States that devote a day to holding these tests on-campus, on a school day, also see increased participation. By eliminating the need for students to travel to an external test center outside of school hours, students find it much easier to take these tests.

In general, measures that seek to reduce accessibility barriers for these tests will help boost participation. As such, we recommend that the College Board seek out states in which they can work with regulators to reduce these barriers.

One such state is Arizona, whose SAT participation rate currently sits around 30%, which makes it a suitable opportunity to explore. Arizona does not yet mandate either the SAT or ACT, and consequently, they also do not have full statewide funding to sponsor all students. They also currently use their own high school assessment, the AzMERIT. The College Board should work with regulators to examine how the SAT can be suitable replacement for the AzMERIT, while supporting ongoing efforts to make testing financially and logistically accessible to all students.

***
## Data dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**state**|*object*|SAT_2017/ACT_2017|State that scores were taken from.|
|**sat_2017_participation**|*float*|SAT_2017|Percentage of students in the state that take the SAT.
|**sat_2017_erw**|*integer*|SAT_2017|Average score obtained in the Evidence-based Reading and Writing subtest. Range: 200-800
|**sat_2017_math**|*integer*|SAT_2017|Average score obtained in the Math subtest. Range: 200-800
|**sat_2017_total**|*integer*|SAT_2017|Average total score obtained in the SAT, as the sum of the ERW and Math subtests. Range: 400-1600
|**act_2017_participation**|*float*|ACT_2017|Percentage of students in the state that take the ACT.
|**act_2017_english**|*float*|ACT_2017|Average score obtained in the English subtest. Range: 1-36
|**act_2017_math**|*float*|ACT_2017|Average score obtained in the Math subtest. Range: 1-36
|**act_2017_reading**|*float*|ACT_2017|Average score obtained in the Math subtest. Range: 1-36
|**act_2017_science**|*float*|ACT_2017|Average score obtained in the Science subtest. Range: 1-36
|**act_2017_composite**|*float*|ACT_2017|Composite score obtained across all 4 subtests. Range: 1-36

Identical features exist for the 2018 SAT and ACT datasets.
