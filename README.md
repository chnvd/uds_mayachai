# Final Project: Urban Data Science 
Spring 2023 project for Urban Data Science

`Maya Deshpande` 
`Chaithra Navada`

## Research Question
 
Was Equity Strategy Neighborhood implementation by San Fransisco MUNI successful in improving neighbourhoods between 2015-16 and 2019? 

## Data Sources

We are collecting data from the following sources:
- MUNI Stop Data from DataSF
- SF Neighbhorhoods from DataSF (SF Find Project)
- Census tract-level income and vehicle ownership data for 2017 and 2019 from the ACS
- Census tract-level race data for 2017 and 2019 from the ACS
- Census tract codes and their corresponding SF neighborhoods from DataSF (Analysis Neighborhoods Project)

## Method
 
We are joining the following characteristics of MUNI stops and theur corresponding neighborhood’s characteristics from 2015-16:
- Median income
- Vehicle Ownership
- Racial Demographic
- In/Not In an Equity Strategy-designated neighborhood

This data serves as training data in a random forest classification model. We train the model on 2017 data to identify whether a stop is in an equity strategy neighborhood or not based on both the stop characteristics and neighborhood characteristics.

We then collect the same MUNI stop and neighborhood data from 2019^, but this time only for equity strategy neighborhoods. This data acts as our test data. We feed this into the clustering model, and see whether it classifies the same stops as in or not in an equity strategy neighborhood based on their updated characteristics. 

If the model classifies our test data as still in equity strategy neighborhoods, then we can conclude that MUNI transit in equity strategy neighborhoods has not improved much since 2015-16. If the model classifies our test data as not in equity strategy neighborhoods, then we can conclude that MUNI transit has improved since 2015-16, and the city can consider graduating such neighborhoods from their “equity strategy” titles. 

_^ We use 2019 data because we are able to draw ACS data through cenpy only until 2019. Expanding this analysis to 2021 will be insightful as it can provide insights on how the pandemic might have lead to changes in the status of ESN._

_We have not yet collected the following data, but would like to include it in a future iteration of this project: Bus speeds, Ridership, and Proximity to Community Anchors_

### Analysis 
##### 2017 Train-Test Model Results
The train-test model run on 2017 has a very high accuracy score. We can see from the confusion matrix that it perfectly identifies 650 observations as negative, and 131 as positive. While this high score could be due to overfitting as the dataset is quite small - a little over 3000 variables it more likely the case that the variables selected are  accurate in determining the `ESN`

#### Classification Modelling

Let us now train the model entirely with 2017 data and predict for 2019 data. We can use this to assess the success of the Muni Equity Strategy Neighbourhood.

We make of use models for the analysis


#### Model 1
Model 1: With string features transformed into categorical variables

##### Model 1 Results
We find that this model perfeclty predicts if the 2019 stops are in `ESN` or not, as seen in the perfect accuracy score. We can see from the confusion matrix that it correctly identifies 2606 observations as negative, and 478 as positive. A conclusion to draw from this would be that ESN desigation has done little to improve the neighborhoods between 2015-16 and 2019

However, as observed in the test-train model accuracy score of 1 could be due to overfitting due to following reasons: the presence of neighbourhood categorical variables is distorting the resutls, as this is perfectly correlated to `ESN` designation, and remains static. Hence this result is spurious and it tells little about if the `ESN` designation continue to be appropriate in 2019. Hence we implement the second model. 


#### Model 2

Model 2 attemts to retain only census dataset variables that are likely to change over the two years. We also transform with an imputer to transform any missing/nan variables as per the trends in the dataset. 

##### Model 2 Results
We find that this model has high accuracy, but it is less than perfect. It correctly identified identifies 2723 observations as negative, and 462 as positive, but classifies 88 as non-ENS despite them being `ESN`. 

### Conclusion
We can take result from `Model 2`  to be an indication of success of the MUNI `ESN` program. The 88 neighbourhoods that were first classified in 2015-16 as having high needs have improved in the intervening years, and now come above the `ESN` theshold. Model predicts these to be `non-ESN`, despite them being classifed as `ESN` in the dataset. The city can consider graduating these neighborhoods from their “equity strategy” titles. 

Neither of the models predict new neighbourhoods to be a `ESN`. We can take this as showing with stronger confidence that the exisiting strategy need is successful in serving `ESN` neighbourhoods that have a need, while not implemeting `ESN` did not have an impact in already well-off neighbourhoods.  
 
 ## Links
[Proposal](https://docs.google.com/document/d/1ZZ_YyN8SOPXLoJtSHEAWqnRYS5ikKO_kZRPhvpu6JSQ/edit#heading=h.bl5su5ntdmg9) 
 
[Proposal Feedback](https://docs.google.com/document/d/1mxfoKShXbY5-FMnL5CRh5xEZgvYAAkdOayPjZA0Dfoc/edit)
 
 ## Work division

`Maya Deshpande` : Data collection, Cleaning and Joins (Section 1.4)
`Chaithra Navada`: Random Forest Model (1.5) 