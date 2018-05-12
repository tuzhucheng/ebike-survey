# ebike-survey

Analysis of Toronto E-Bike survey response results to predict if a household has access to a private motorized vehicle (yes/no).

* `analysis_and_preprocessing.ipynb`: This file is used for exploratory analysis and data preprocessing, cleaning, etc.
* `modelling.ipynb`: This file is used to build the models

20% of the data is left out for testing. For the remaining 80% of the data, 5-fold cross validation is used for training/validation.

## Model selection

The following models are considered:

* Baseline: majority classifier
* Logistic Regression: simple model that's fast to train and easy to interpret
* SVM with RBF kernel and polynomial kernel: can model non-linear decision boundaries
* Random Forest: forest of decision trees that can model non-linear decision boundaries
* Neural Network (MLP): can model non-linear decision boundaries
* Gradient Boosting: ensemble of decision trees that can optimize arbitrary differentiable loss functions

I chose the gradient boosting model. Model selection is chosen based on the model that has the best mean ROC AUC on the validation sets. Gradient boosting led to the best AUC on the validation set (see `modelling.ipynb`). The AUC of the testing set is 0.895.

## Missing values

There are 2238 rows in the dataset in total. Fields that have < 2238 non-null objects have missing values.

```
timestamp                 2238 non-null object
age                       2234 non-null object
sex                       2221 non-null object
health                    2227 non-null object
education                 2220 non-null object
income                    2178 non-null object
employment                2223 non-null object
district                  2237 non-null object
daily_travel_distance     2237 non-null object
commute_time              2237 non-null object
transportation            2238 non-null object
vehicles                  2238 non-null object
statements                2238 non-null object
trail_activity            2238 non-null object
speed_limit_aware         2238 non-null object
conflict                  2238 non-null object
speeding_demand_action    2237 non-null object
ebike_multiuse_path       2238 non-null object
bicycle_lane              2238 non-null object
ebike_bicycle_lane        2238 non-null object
sidewalk                  2238 non-null object
mobility_devices          2232 non-null object
```

`income` had the most number of missing values and it is intuitively important for predicting the label. However, `income` can be inferred from the level of `education` - income is not random.
We find that the median income for respondents with "High school diploma" or "College or trade school diploma" is "$60K to $79K".
The median income for respondents with "University degree" is "$80K to $99K".
The median income for respondents with "Post graduate" is "$100K+".

We impute the missing values for `income` based on the median income of the corresponding `education` level if `education` is not missing. If both `education` and `income` are missing, we drop those examples (only 7 in total).

For `sex`, we use the "Other" category for values that are neither "Male" nor "Female", which can take care of missing values. For `health` missing values, we treat them as "Poor" as well as the conditions that only appear once since they all indicate the existence of some health condition. For treatment of other missing values, please refer to the code in `analysis_and_preprocessing.ipynb`.

## Significant features

## Survey redesign
