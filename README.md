# spaceship-titanic, by [Andres Perez](https://www.andresperez.info/)
My code for submissions to kaggle competition [Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic/overview).

Using this notebook for guidance: [Geunho](https://www.kaggle.com/code/arootda/pycaret-visualization-optimization-0-81/data)

## Data Dictionary
- train.csv - Personal records for about two-thirds (~8700) of the passengers, to be used as training data.
    - PassengerId - A unique Id for each passenger. Each Id takes the form gggg_pp where gggg indicates a group the passenger is travelling with and pp is their number within the group. People in a group are often family members, but not always.
    - HomePlanet - The planet the passenger departed from, typically their planet of permanent residence.
    - CryoSleep - Indicates whether the passenger elected to be put into suspended animation for the duration of the voyage. Passengers in cryosleep are confined to their cabins.
    - Cabin - The cabin number where the passenger is staying. Takes the form deck/num/side, where side can be either P for Port or S for Starboard.
    - Destination - The planet the passenger will be debarking to.
    - Age - The age of the passenger.
    - VIP - Whether the passenger has paid for special VIP service during the voyage.
    - RoomService, FoodCourt, ShoppingMall, Spa, VRDeck - Amount the passenger has billed at each of the Spaceship Titanic's many luxury amenities.
    - Name - The first and last names of the passenger.
    - Transported - Whether the passenger was transported to another dimension. This is the target, the column you are trying to predict.
- test.csv - Personal records for the remaining one-third (~4300) of the passengers, to be used as test data. Your task is to predict the value of Transported for the passengers in this set.
- sample_submission.csv - A submission file in the correct format.
    - PassengerId - Id for each passenger in the test set.
    - Transported - The target. For each passenger, predict either True or False.

## Data Collection
Data downloaded from kaggle consists of a [labeled training set](./data/train.csv), [unlabeled testing set](./data/test.csv) and a [sample submission csv](./data/sample_submission.csv).

## EDA
1. Combined Train and Test data for EDA
1. Checked for missing values
    - Features have ~2% missing values. Must impute.
    - Use the mean of numerical features to fill missing values.
    - Use the mode of categorical features to fill missing values.
    - Other fill methods will also be explored, as done by other kaggle competitors
1. Identified target: "Transported"
1. Numerical features: ["Age", "RoomService", "FoodCourt", "ShoppingMall", "Spa", "VRDeck"]
1. Categorical features: [ "PassengerId", "HomePlanet", "CryoSleep", "Cabin", "Destination", "VIP", "Name"]
1. Explored Target and Feature Distributions
    - Target is balanced.
    - Split PassengerId and Name to create IsFamily feature, which appears to be useful.
    - HomePlanet, CryoSleep, and Destination distributions by target also appear useful.
    - Split Cabin by Deck, Number and Side, distributions by target also appear useful.
    - VIP does not appear to be very useful.
    - Age distribution by target also shows promise. Creating age group features should be useful.
    - Grouped spending features, DidNotSpend feature appears useful.

## Missing Values
1. Imputed missing values in categorical features using the mode of each feature.
1. Imputed missing values in 'Age' feature using the mean.
1. Imputed missing values in spending with 0.

## Feature Engineering
1. Created IsFamily feature based on Group feature extracted from PassengerId
1. Created Deck, Number, and Side features extracted from Cabin.
1. Created AgeBin categories from Age feature
1. Created Spent feature based on Total Spending
1. Dropped PassengerId, Name, and Cabin.

## Encoding Categorical Features
1. Used Label Encoder to encode categorical features.
1. Formatted boolean features as integers.

## Train, Test split
1. Split data back to it's original train and test sets.
1. Created a validation set.

## Modeling
1. Established a 50.36% baseline by predicting the most common class.
1. Created a training and scoring function to evaluate individual models based on training and validation accuracy.
1. Trained Logistic Regression and CatBoost models.
1. Submitted CatBoost predictions with default parameters achieving 80.50% accuracy on kaggle.
