# Machine-Learning-with-XGBoost

# Assignment 2: XGBoost Introduction
---
## XGBoost

It stands for `eXtreme Gradient Boosting` which enables us to use `Gradient Boosted Decision Tree algorithms`. A continuous process of calculating errors, predictions, and Ensemble is what Gradient Boosted Decision Tree does.

-	**_Errors:** Taking an existing model and calculating errors from each observation of the dataset to build a new model to predict these errors._

-	**_Predictions:** Adding up previous predictions, calculating new errors from those, or to ensemble them._

-	**_Ensemble:** Putting together all the models from which errors can be calculated from select models to create better models._

### Setting up the environment

-	_To set up the environment functions like XGBoost and tidyverse are needed to be installed and called as libraries._

-	_The data here represents outbreaks of animal diseases, through this data we may be able to predict what animal diseases can make humans sick._

-	_To get a random sample while splitting into testing and training set, shuffling needs to be done._

#### Preparing the data & selecting features

One of the limitations of XGBoost is it can’t operate on a raw data, the data needs to be in a `matrix format` i.e., dataframe in `numeric format` (DMatrix for XGBoost). The data used for this experiment is not in a matrix or all numeric format which is why cleaning is to be done by,

   1.	**_Remove information about the target variable from the training data:** Removal of information is necessary because this’ll impact on the predicted outcome and give us accurate results (avoid leakage)._

   2.	**_Reduce the amount of redundant information:** Eliminating redundant information which is of no use in order to predict and non-numeric variables to create a matrix._

   3.	**_Convert categorical information (like country) to a numeric format:** To convert non-numeric variables into numeric one-hot encoding can be used which will categories each observation and shuffle them in 0 (belongs to the column) & 1 (doesn’t belong to the column)_

   4.	**_Split dataset into testing and training subsets:** Splitting the dataset into training (70%) & testing (30%) to check the robustness of the model for prediction._

   5.	**_Convert the cleaned dataframe to a Dmatrix:** Converting matrixes into dmatrixes for it to train the model in multiple cores._

#### Training our model

After cleaning the dataset and splitting into training & testing, `training` on the one model can begin and necessary changes may also be made. In order to train the model, it needs to know few aspects:

1.	_**What training data to use**: a dmatrix format is required to train the dataset_

2.	_**The number of training rounds:** The number of times a Naïve model should be improved by adding additional models (Fig. 1: one circle = 1 boosting)_

3.	_**What the objective function is:** What task is to be performed, depending on the dataset (linear, multiple or logistic regression)_

Running the model twice may give the same results which leads to how accurate is the `testing data` which the model hasn’t seen before.

#### Tuning the model

If the model’s error is low then there’s no worries, but if it is slightly high then `over-fitting` may occur which means the model relies heavily on randomness/noise of training set for its classification. One way of avoiding over-fitting is by reducing the layers of decision tree to make it less complex (no smaller pieces in each layer) or another technique is to use regularisation term, which will measure how much additional split is required to reduce any loss & add to ensemble.

To see if the model is `under-fitting` or using important information to produce the output,

1.	**_Imbalanced classes:** It is the proportion to which the categories are in volume, since one category can impact on the output if it is more than the other._

2.	**_More training rounds:** Early or longer training may result in high error rate which can be guarded by early_stopping_rounds which will stop the training if no improvements._

#### Examining the model

XGBoost is advantageous because of its `built-in` functions helping us to figure why the model behaves such way. One way of examining the model is through **combination of representation** of all decision trees stacked over one another and pick the often showed up node. In a decision tree, the left is the top of tree and right is the bottom. In_domestic has the highest quality (number beside the name) which means it was very important and higher in the tree.

The value beside Leaf is the average value returned if all trees’ certain observation were to end up on that leaf; since this is a logistic model, the value showed is log-odds which could be changed into probabilities. For a quick way i.e., importance matrix can help in observing the important feathers, through this the interpretation becomes easy because the X-axis denotes to weighted gains (high gains very important/less gains less helpful) wherein it sums each feather to 1, and it tells us how informative each feather was when looked at the ensemble. And the results show that coming in contact with a domestic animal will lead to human getting sick.
