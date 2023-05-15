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

### <AlpahabetSoupCharity_Optimisation_keras_tuner.ipynb> for use of an autotuner to find best model hyperparameters.
### <AlpahabetSoupCharity_Optimisation.ipynb> for the process described below.

 - The "IS_SUCCESSFUL" column, was the y target variable for the model. 
 - There were 18261 `1` successful labels and 16038 `0` unsuccessful labels. This indicated a fairly well-balanced column of data as the target variable.
 - All other columns, excluding "EIN", are the X variable or features for the model.

 - The "EIN" column was removed from the input data because it was an identification column ( each EIN was a unique value) and neither a target nor feature. 
 - The "NAME" column is also an identification column, but I added this into the input data as the value-counts of this column (not all names were unique) indicated that many organisations had applied for funding on multiple occassions, hence the frequency of their application for funding may contribute to success in being funded.

 - The "NAME" column had any organisations that applied less than 293 times (value_counts) for funding, "binned" together in a new value called "Other". So there were 10 unique values for this column.
 - The "CLASSIFICATION" column had 71 unique values, so any values with less than 777 value_counts, were  "binned" together in a new value called "Other". So there were 7 unique values for this column.
  - The "APPLICATION" column had 17 unique values, so any values with less than 156 value_counts, were  "binned" together in a new value called "Other". So there were 10 unique values for this column.
  - The "AFFILIATION" column had 6 unique values, so any values with less than 15705 value_counts, were  "binned" together in a new value called "Other". So there were 3 unique values for this column.
  - The "INCOME_AMT" column had 9 unique values, so any values with less than 3374 value_counts, were  "binned" together in a new value called "Other". So there were 4 unique values for this column.
  - The "USE_CASE" column had 5 unique values, so any values with less than 5671 value_counts, were  "binned" together in a new value called "Other". So there were 3 unique values for this column.
   - The "INCOME" column had 4 unique values, and were not binned in any way.

  - I used the OneHotEncoder to convert all categorical columns into numerical data, as an alternative method to using get_dummies. These columns were then merged with the numerical columns.
  - I then chose to drop the column 'SPECIAL_CONSIDERATIONS_N' as values for this were already contained in the 'SPECIAL_CONSIDERATIONS_Y' column.
  - The final DataFrame had 45 columns.
  - Data was split using "train_test_split".
  - Data was then scaled as the "ASK_AMT" column was a much larger integer compared with all other columns.


### Compiling, Training, and Evaluating the Model

 - With 45 columns I chose between 2-3 times this number in the first input layer, also experimenting with LeakyReLu and tanh activation functions. I got best results with 90 neurons in the first layer and a tanh activation function.
 - The 2nd layer had less than half the number of neurons as the first layer and I experimented with LeakyReLu and tanh activation functions. I got best results with 45 neurons and a tanh activation function. 
 - I was very close to achieving the target model performance of 75% and achieved an accuracy of 74.54%.
 
 The steps I took in my attempts to increase model performance included:
 - Reducing the features in the DataFrame.
 - Increasing the number of neurons/nodes in each hidden layer. 
 - Adding hidden layers to increase the depth of the net.
 - Experimenting with optimising the model with adamW and a learning-rate.
 - Experimenting with a dropout activation in a layer.
 - Experimenting with tanh and leakyrelu activation fucntion in each, all or alternating layers.
 - Increasing epochs.
 - Changing the train_test_split with train-size = 0.2, rather than the deafulkt setting of 0.25.

## Summary.

The deep learning model optimisation <AlpahabetSoupCharity_Optimisation.ipynb> achieved an improved accuracy and reduced loss when compared with the first model <AlpahabetSoupCharity.ipynb>.

First model
Loss: 0.5581400394439697, Accuracy: 0.7292128205299377

Optimisation model
Loss: 0.517242431640625, Accuracy: 0.745306134223938

I would recommend the use of a logistic regression model, a support vector machine learning model or a decision tree to improve prediction accuracy with this classification problem of what features contribute to improved success in getting funding from the Alphabet Soup organisation.

### Enjoy marking!
### Sandra