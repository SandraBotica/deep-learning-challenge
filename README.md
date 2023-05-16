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

<AlpahabetSoupCharity.ipynb> for the original machine learning model.
<AlpahabetSoupCharity_Optimisation_keras_tuner.ipynb> for use of an autotuner to find best model hyperparameters.
<AlpahabetSoupCharity_Optimisation.ipynb> for the process described below.

## Results
## Data Preprocessing
### What variable(s) are the target(s) for your model?
 - The "IS_SUCCESSFUL" column, was the y target variable for the model. 
 - There were 18261 `1` successful labels and 16038 `0` unsuccessful labels. This indicated a fairly well-balanced column of data as the target variable.
### What variable(s) are the features for your model?
 - All other columns, excluding "EIN", are the X variable or features for the model.
### What variable(s) should be removed from the input data because they are neither targets nor features?
 - The "EIN" column was removed from the input data because it was an identification column ( each EIN was a unique value) and neither a target nor feature. 
 - The "NAME" column is also an identification column, but I added this into the input data as the value-counts of this column (not all names were unique) indicated that many organisations had applied for funding on multiple occassions, hence the frequency of their application for funding may contribute to success in being funded.

 - The "NAME" column had any organisations that applied less than 206 times (value_counts) for funding, "binned" together in a new value called "Other". So there were 15 unique values for this column.
 - The "CLASSIFICATION" column had 71 unique values, so any values with less than 58 value_counts, were  "binned" together in a new value called "Other". So there were 15 unique values for this column.
  - The "APPLICATION" column had 17 unique values, I kept all of these, no binning.
  - The "AFFILIATION" column had 6 unique values, I kept all of these, no binning.
  - The "INCOME_AMT" column had 9 unique values, I kept all of these, no binning.
  - The "USE_CASE" column had 5 unique values, I kept all of these, no binning.
   - The "ORGANISATION" column had 4 unique values, I kept all of these, no binning.

  - I used the OneHotEncoder to convert all categorical columns into numerical data, as an alternative method to using get_dummies. These columns were then merged with the numerical columns.
  - I then chose to drop the column 'SPECIAL_CONSIDERATIONS_N' as values for this were already contained in the 'SPECIAL_CONSIDERATIONS_Y' column.
  - The final DataFrame had 75 columns.
  - Data was split using "train_test_split".
  - Data was then scaled as the "ASK_AMT" column was a much larger integer compared with all other columns.
## Compiling, Training, and Evaluating the Model
### How many neurons, layers, and activation functions did you select for your neural network model, and why?
 - The features for the model were 74 in total.
 - The length of X-train, 74, was the input-dimensions for the input layer, with 74 neurons. I experimented with relu, LeakyReLu and tanh activation functions, and got best results with a tanh activation function.
 - In the 2nd hidden layer I chose to use two thirds the input layer of neurons, selecting 50. I experimented with relu, LeakyReLu and tanh activation functions, and got best results with a tanh activation function. 
 - In the output layer there was 1 neuron and a sigmoid activation function used.
 - There were 9351 parameters in this model.

 - I was also able to create a callback that saved the model weights every five epochs. These were saved in a checkpoint folder in content in colab.
### Were you able to achieve the target model performance?
 - I am so EXCITED to say I achieved the target model performance of 75% accuracy.
### What steps did you take in your attempts to increase model performance?
 - Experimenting with binning fewer features so as to have more columns in the Dataframe.
 - Increasing the number of neurons/nodes in each hidden layer. 
 - I experimented with a 3rd hidden layer, but this did not improve accuracy or reduce loss.
 - I tried an optimisation with adamW and a learning-rate.
 - I also experimented with a dropout activation in alayer.
 - I used relu, tanh and leakyrelu activation fucntion in each, all or alternating layers.
 - I also experimented with increasing epochs.
 - Changing the train_test_split with train-size = 0.2, rather than the deafult setting of 0.25, was also tried, but this did not help the model convergence.

## Summary.

The deep learning model optimisation <AlpahabetSoupCharity_Optimisation.ipynb> achieved an improved accuracy and reduced loss when compared with the first model <AlpahabetSoupCharity.ipynb>.

First model
Loss: 0.5581400394439697, Accuracy: 0.7292128205299377

Optimisation model
Loss: 0.5132946372032166, Accuracy: 0.7500874400138855

I also ran a keras tuner to find the best 3 model hyperparameters, <AlpahabetSoupCharity_Optimisation_keras_tuner.ipynb>. 

I would recommend the use of a logistic regression model, a support vector machine learning model or a decision tree to improve prediction accuracy with this classification problem of what features contribute to improved success in getting funding from the Alphabet Soup organisation.

### Enjoy marking! Sandra