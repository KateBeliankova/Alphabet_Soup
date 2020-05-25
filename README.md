# Alphabet soup venture campaign

## Background

This project was aimed with the help of Deep Learning model to predict whether or not an applicant will be successful if funded by Alphabet Soup.

## Preprocessing of the dataset
Within the dataset are a number of columns that capture metadata about each organization such as the following:

- EIN and NAME—Identification columns
- APPLICATION_TYPE—Alphabet Soup application type
- AFFILIATION—Affiliated sector of industry
- CLASSIFICATION—Government organization classification
- USE_CASE—Use case for funding
- ORGANIZATION—Organization type
- STATUS—Active status
- INCOME_AMT—Income classification
- SPECIAL_CONSIDERATIONS—Special consideration for application
- ASK_AMT—Funding amount requested
- IS_SUCCESSFUL—Was the money used effectively

In the model was used IS_SUCCESSFUL variable as target variable
It was decided to use in dataframe EIN number as index. NAME variable was removed from the dataset as it supposed to have no impact on target variable.

Also it was noticed that variables APPLICATION_TYPE and CLASSIFICATION have too many unique values, so it was decided to bit some values in this columns into “Other” group.

Also all categorical variables were one-hot encoded and standardized.

The variable ASK_AMT needed also was preprocessed: values in this variable was binned into two groups –  “5000 or less” and “more than 5000”. It was done to standardize weights with other variables .

## Building Deep Learning model
As we have pretty large data set (almost 40,000 cases) it was decided to use deep learning model. 
As the model achieved only 70% accuracy, some modifications were tried.
1.	Number of hidden layers and neurons: it was tried in the model from 1 to 4 hidden layers. The highest accuracy was achieved with 3 hidden layers (first hidden layer contains 20 neurons, the second – 10, and the third --5 )
2.	Activation functions: the primary model had relu activation function on all hidden layers, but as our final dataframe mostly includes the binary data it was tried to use sigmoid and tanh functions. The best results were achieved with using relu function on the first and second hidded variables and sigmoin on the third hidden layer. 
3.	Number of epochs: during the first attempt was used 100 epochs, and accuracy was lower 75% so number of epochs was increased to 200, but accuracy in this case decreased. It was decided to try epochs = 50 and this model showed the best performance.
4.	Features: to increase model accuracy it was decided to remove some variables, that might be noisy. So it was additionally removed  columns “STATUS” (as almost all cases have active status) and “SPECIAL_CONSIDERATION_YES”(as it just shows opposite information to “SPECIAL_CONSIDERATION_NO”)
Also it was tried to change binning of the variables “ASK_AMT” and “APPLICATION_TYPE” but it doesn’t improved the model, so changes weren’t implemented in the final model. 
## Takeaways
Because of applied modifications the accuracy of the final model was increased from 70.1% to 73.8%
