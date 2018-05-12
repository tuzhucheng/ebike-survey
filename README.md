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

## Significant features

## Survey redesign
