# Intro to Gradient Boosting

# Here I will learn how gradient boosting combines several models into a strong model.

## Learning objectives

- Understand the conceptual difference between bagging and boosting ensembles
- Understand how gradient boosting works for regression tasks
- Learn how to tune the key hyperparameters of gradient boosting ensembles

## What is Boosting?

Boosting methods train the models sequentially. Eaach model is chosen to improve the overall performance.

![image](https://user-images.githubusercontent.com/86930309/231586031-187aa0b3-c338-40bf-bfbb-3b9d97708257.png)

## 1. Import Libraries

## 2. Generate Data

- Graph of our training set:

![image](https://user-images.githubusercontent.com/86930309/231588098-e0b1d58b-4577-469f-b5eb-2be60c83bbdc.png)

## 3. Build a Model on the Data

- a. Create a shallow decision tree:

![image](https://user-images.githubusercontent.com/86930309/231588637-656187dd-a811-49a2-9422-e36be0dfc68b.png)

The value in each node is the average target value of the training examples.

- b. Create a new column to that predicts the y based upon the X. 

- C. Graph of predictions on the trainign set:

![image](https://user-images.githubusercontent.com/86930309/231589824-8fd6d6e3-fc98-4e6b-a91c-ec2713293eec.png)

## 4. Build a Model on the Residuals

The weak model above is barely able to capture the structure of the data (i.e. it has high bias). However, we can improve the predictions by training a second regression tree on the residual errors made by the first tree.

## 5. Create a Composite Model

- a. Now we have an ensemble consisting of two trees. We can get the predictions from the ensemble by simply summing the predictions across all trees.

- b. We can plot the predictions of both our second tree on the residuals, along with the predictions from the ensemble on the training set:

![image](https://user-images.githubusercontent.com/86930309/232161777-4bada28a-8da4-47ef-afe3-0d236eb8d3ff.png)

The ensemble's predictions have improved.

## 6. Rinse and repeat

 Adding more models to the ensemble improves the predictions:

![image](https://user-images.githubusercontent.com/86930309/232162188-bd483f71-5a85-4fd5-9ce1-5da57c3cd00a.png)

## 7. Gradient boosting with scikit-learn

Manually building up the gradient boosting ensemble is a drag, so in practice it is better to make use of scikit-learn's GradientBoostingRegressor class. This is what we get when we use the parameters max_depth=2, n_estimators=3, learning_rate=1.0:

![image](https://user-images.githubusercontent.com/86930309/232163249-bd605b86-4601-4c42-915c-a31f7d3aaaf5.png)

- a. Choosing hyperparameters

Two main hyperparameters: 

learning_rate

n_estimators

- b. Effect of learning rate

let's train two ensembles at different extremes. One with 3 and one with 200 n_estimators.

![image](https://user-images.githubusercontent.com/86930309/232165145-43ea9f12-76d0-4ba3-a854-673ba3f9d2b4.png)

- c. Early stopping

For fixed learing rate, we can find the optimal number of trees using a technique known as "early stoppping". Here the idea is to use a validation set to measure how the error decreases as we add more trees and find the optimal point from the curve:

The best n estimators for this dataset is 56.

![image](https://user-images.githubusercontent.com/86930309/232165379-eaf585c9-7054-453a-a24c-b5f50bc2f450.png)

It is better to actually stop the training when the early stopping criterion is met, instead of training many redundant models. In scikit-learn, this is configured by setting warm_start=True which allows for incremental training and can be use to stop the training loop when some threshold is met.

The optimal number of trees is 60:

![image](https://user-images.githubusercontent.com/86930309/232165886-9144492b-57ba-4980-b1eb-f8468638c41e.png)

## 8. Final Exercises

Use scikit-learn's GradientBoostingClassifier to explore how the algorithm's hyperparameters influence the decision boundary on the following synthetic dataset for binary classification.

![image](https://user-images.githubusercontent.com/86930309/232166187-c31e22ec-cb85-4981-9c00-1c1df734d52e.png)



