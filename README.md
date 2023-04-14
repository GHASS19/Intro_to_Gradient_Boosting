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




