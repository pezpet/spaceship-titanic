# spaceship-titanic
My code for submissions to kaggle competition [Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic/overview).

Using this notebook for guidance: [Geunho](https://www.kaggle.com/code/arootda/pycaret-visualization-optimization-0-81/data)

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
