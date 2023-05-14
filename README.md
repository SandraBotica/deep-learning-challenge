## Module 21 Report - deep-learning-challenge.

## Overview.

## The purpose of this analysis was to use my knowledge of machine learning and neural networks to create a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup.

The funding information of more than 34,000 organisations that have received funding from Alphabet Soup over the years was  imported from the <charity_data.csv>  and included (12 columns and 34298 rows, excluding the Header):
 - EIN
 - NAME
 - APPLICATION_TYPE
 - AFFILIATION
 - CLASSIFICATION
 - USE_CASE
 - ORGANIZATION
 - STATUS
 - INCOME_AMT
 - SPECIAL_CONSIDERATIONS
 - ASK_AMT
 - IS_SUCCESSFUL (`0` label = unsuccessful, `1` label = successful)

## Results.

### Data Preprocessing

### <AlpahabetSoupCharity.ipynb> for the original machine learning model.
### <AlpahabetSoupCharity_Optimisation.ipynb> for the process described below.

 - The "IS_SUCCESSFUL" column, was the y target variable for the model. 
 - There were 18261 `1` successful labels and 16038 `0` unsuccessful labels. This indicated a fairly well-balanced column of data as the target variable.
 - All other columns, excluding "EIN", were the X variable or features for the model.
 - The "EIN" column was removed from the input data because it was an identification column and neither a target nor feature. 
 - The "NAME" column is also an identification column, but I added this into the input data as the value-counts of this column indicated that many organisations had applied for funding on multiple occassions, hence the frequency of their application for funding may contribute to success in being funded.
 - The "NAME" column had any organisations that applied less than 206 times (value_counts) for funding, "binned" together in a new value called "Other". So there were 15 unique values for this column.
 - The "CLASSIFICATION" column had 71 unique values, so any values with less than 116 value_counts, were  "binned" together in a new value called "Other". So there were 10 unique values for this column.
  - The "APPLICATION" column had 17 unique values, but I decided to keep all of these as the different types of application could prove to contribute to successful applications for funding or not. Hence I thought it would be important in the prediction model.
  - I used the OneHotEncoder to convert all categorical columns into numerical data, as an alternative method to using get_dummies. These columns were then merged with the numerical columns.
  - I then chose to drop the column 'SPECIAL_CONSIDERATIONS_N' as values for this were already contained in the 'SPECIAL_CONSIDERATIONS_Y' column.
  - The final DataFrame had 65 columns.
  - Data was split using "train_test_split".
  - Data was then scaled as the "ASK_AMT" column was a much larger integer compared with all other columns.


### Compiling, Training, and Evaluating the Model

 - With 70 columns I chose between 2-3 times this number in the first input layer, also experimenting with relu and tanh activation functions. I got best results with 130 neurons in the first layer and a tanh activation function.
 - The 2nd layer had less than half the number of neurons as the first layer and I experimented with relu and tanh activation functions. I got best results with 55 neurons and a tanh activation function. 
 - I was very close to achieving the target model performance of 75% and achieved an accuracy of 74.92%.
 
 The steps I took in my attempts to increase model performance included:
 - Collecting more data for the input dataset to increase the width of the net e.g. adding "NAME" column into dataset, keeping all the unique values for the "APPLICATION_TYPE" column.
 - Increasing the number of neurons in each hidden layer, based on the columns in the preprocessed DataFrame. 
 - Adding hidden layers to increase the depth of the net.
 - Experimenting with optimising the model with adamW and a learning-rate.
 - Experimenting with a dropout activation in a layer.
 - Experimenting with tanh and relu activation fucntion in each, all or alternating layers.
 - Decreasing and increasing epochs.
 - Changing the train_test_split with train-size = 0.2, rather than the deafulkt setting of 0.25.

## Summary.

Summarise the overall results of the deep learning model. Include a recommendation for how a different model could solve this classification problem, and then explain your recommendation.

### Enjoy marking!
### Sandra