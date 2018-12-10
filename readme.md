# Predicting Serious Mental Illness with a Regression Model

## Project Definition:
Can we predict the number of Serious Mental Illnesses (SMI)† in the U.S with certain features?

## Features:
- Number of drug arrests
- White, Black, and Hispanic population
- Median Income
- Male Percentage
- Unemployment Rate
- Number of drug labs found††
- Whether the state was Republican or Democratic

Note:
† Serious mental illness (SMI), as defined by the National Survey on Drug Use (NSDUH) is defined as having a diagnosable mental, behavioral, or emotional disorder, other than a developmental or substance use disorder, as assessed by the Mental Health Surveillance Study (MHSS) Structured Clinical Interview for the Diagnostic and Statistical Manual of Mental Disorders—Fourth Edition—Research Version—Axis I Disorders (MHSS-SCID), which is based on the 4th edition of the Diagnostic and Statistical Manual of Mental Disorders (DSM-IV). SMI includes individuals with diagnoses resulting in serious functional impairment. For details, see Section B of the ""2011-2012 NSDUH: Guide to State Tables and
Summary of Small Area Estimation Methodology"" at http://www.samhsa.gov/data/."

†† DEA's website contains addresses of some locations where law enforcement agencies reported they found chemicals or other items that indicated the presence of either clandestine drug laboratories or dumpsites. In most cases, the source of the entries is not the Department, and the Department has not verified the entry and does not guarantee its accuracy.

## Constructing the Data Frame:
the data frame consists of the features data for years 2014-2017 segmented by states. Selecting the certain features was a mix of intuition and what data was available. Although, as noted, the SMI does not include substance use disorders, we want to test if the number of drug arrests can be one of the predictors of SMI #s in a state. We also wanted certain independent variables, such as population demographics (gender and race). It could be argued that unemployment rate is not independent of the other features, but that is why we check the correlation amongst all the independent variables. We're also curious to see if the number of drug labs found in a state is correlated to the number of SMI within the state. As well as determining whether the political stance of a state is a good indicator of SMI numbers.

### Dataframe screenshot:
<img src="images/dataframe.png" style="width: 500px;"/>

### Matrix screenshot of pair plots of the features and dependent variable:
<img src="images/matrix.png" style="width: 500px;"/>

As you can see in the first column, where the dependent variable is on the y-axis, there are some relationships visible before doing any feature selection/engineering. i.e. the relationship between SMI and drug arrests seems to be linear.

## Regression Model:

For our regression model, we went through several iterations. The difference amongst those iterations are detailed below.

### Iteration 1:
<img src="images/iter1.png" style="width: 500px;"/>

Our R-squared, from the model is 0.826. That's a good fit, but the p-values for the featured variables are above 0.05. We decided to scale our split data (train set and test set) and use a polynomial fit with a degree = 2.

### Iteration 2:
<img src="images/iter2.png" style="width: 500px;"/>

Our R-squared, from this model is 0.923. This is better than our previous model. There are still some p-values way above 0.05; we have to get rid of these variables. But because there are so many variables to look at, we'll use a Features Filtered Method: Variance Test.

### Iteration 3:
<img src="images/iter3.png" style="width: 500px;"/>

Our p-values were still above 0.05, despite getting rid of some of our data. So we turn to a wrapper method.

### Iteration 4:
<img src="images/iter4.png" style="width: 500px;"/>

Our R-squared looks great, and most of our p-values are well below 0.05, except one variable. We decide to get rid of this variable.

### Iteration 5:
<img src="images/iter5.png" style="width: 500px;"/>

Our R-squared value is 0.865, all the p-values of the features are lower than 0.05, and we are satisfied with our RMSE and stddev values. We therefore conclude our Regression Model Analysis and found our best fit model for our data.

Below are some illustrations of our final linear model.

#### Residual Graph:
<img src="images/residualgraph.png" style="width: 500px;"/>

#### Heat Map:
<img src="images/heatmap.png" style="width: 500px;"/>

Regression Model:
<img src="images/regressionmodel.png" style="width: 500px;"/>

Our model tells us that predicting the number of serious mental illness population for a given state in a given year can be determined using the following formula. e.g. If the unemployment rate was to go up 1%, smi counts will go down 20.1. It's an interesting interpretation to finding the number of smi cases. It should be noted that for our final model the root-mean-squared-error (RMSE) was 70.72, and our standardized RMSE was 0.35. This means that our predicted value will be on average +/-70.72 from the actual value.

We also did a cross validation (K-Fold) on our train data, and got an average R-squared value of 0.58. This means that our model explains 58% of the variability of the response data around its mean.

(Please look at our Regression file to see a quick Lasso and Ridge analysis)
