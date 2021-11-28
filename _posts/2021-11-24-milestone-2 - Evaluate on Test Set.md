---
layout: post
title: NHL Data Science Project - Milestone 2 - Evaluate on Test Set
---


# Evaluate on Test Set

## Q1: Model Evaluation Using 2019/20 Regular Season Games


The three logistic regression models, the best XGBoost model, and the best overall model were retrieved from comet.ml and used to predict the test set's probability of goals. The test set was divided and grouped by regular season games and postseason games. Two separate classifier quality charts were generated as a result.

The test set prediction accuracy and AUC value for the regular season games matched results obtained from the validation set for all five models. As shown below, the classifier quality charts confirm that there was no significant variation in model performance. Both the neural network model and the XGBoost model had comparable performance and both outperformed the remaining models. The logistic regression model trained on distance and angle achieved the same performance as the logistic regression model trained on distance only. The logistic regression model trained on angle only remained to be the worst performing model. As a result, it can be concluded that the validation set is a good representation of the general data.

|                                        | Accuracy | AUC |
| Logistic Regression Distance Only      |       90       |      0.70     |
| Logistic Regression Angle Only         |       90       |      0.51     |
| Logistic Regression Distance and Angle |       90       |      0.70     |
| XGBoost Model with SHAP                |       92       |      0.83     |
| Neural Network - Advance Features      |       92       |      0.84     |




![Regular Season Test Set](/Images/M2_ET_Q1_M2_ET_Q1_Regular_Testset.png)



## Q2: Model Evaluation Using 2019/20 Post Season Games 

The model performance results evaluated using the postseason games were similar to the results obtained through the regular season games. The table below shows that there was only a minor increase in prediction accuracy and the AUC values remained the same. The curves in the classifier quality charts generated using the postseason game predictions appear to be noisier than the curves in the previous charts. This observed granularity is attributed to the lower number of games in the dataset. One noticeable difference can be observed between the two reliability charts. While the general shape of the curves remained similar, both the neural network model and the XGBoost model were unable to produce any probabilities above 0.6. This is also attributed to the lower number of samples available since the reliability chart bins the probabilities to produce a more meaningful representation. The test set suggests that all five models were not overfitted and are generalized predictors of the data set.

|                                        | Accuracy | AUC |
| Logistic Regression Distance Only      |       91       |      0.70     |
| Logistic Regression Angle Only         |       91       |      0.51     |
| Logistic Regression Distance and Angle |       91       |      0.70     |
| XGBoost Model with SHAP                |       93       |      0.83     |
| Neural Network - Advance Features      |       93       |      0.84     |



![Post Season Test Set](/Images/M2_ET_Q1_M2_ET_Q2_Post_Testset.png)







