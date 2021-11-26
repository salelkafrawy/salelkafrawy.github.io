---
layout: post
title: NHL Data Science Project - Milestone 2 - Advanced Models
---


# Advanced Models

## Q1: XGBoost Trained on Distance and Angle Features

The XGBoost library is utilized to create the gradient boosted tree classifier, an ensembling method that combines outputs from individual trees to generate the final prediction. A baseline XGBoost model is created as instructed. This baseline model uses the same training/validation setup as the logistic regression models and is trained only on distance and angle features. Compare to the Logistic Regression model trained on distance and angle, the only difference is that the input features are not normalized. This decision is made based on the fact that decision trees are usually not affected by any monotonic transformation. 

While the baseline XGBoost model achieves a very similar accuracy compare to the its Logistic Regssion counterpart (~90%), the confusion matrix reveals that the prediction of goals by this model is non-zero. Plotting the baseline XGBoost model with the Logistis Regression model on the four performance evaluation figures confirms that the XGBoost model has a marginal performance advantage over the Logistis Regression model (See below). Most notably, the reliability curve shows that the XGBoost model produces more higher predicted Probabilities that are inline with the perfectly calibrated line. 

| Actual: No Goal |        60148       |        20        |
|   Actual: Goal  |        6203        |        19        |
|                 | Predicted: No Goal | Predicted: Goal |


![XGBoost Baseline](/Images/M2_AM_Q2_XGBoost_Baseline.png)

### Comet.ml link:
Experiment entry: https://www.comet.ml/tim-k-lee/ift6758-hockey/70a252e382c74d94ae7b2ff56e3ec7bf




## Q2: XGBoost Trained on New Features and Hyperparameter Tuning




In your blog post, discuss your hyperparameter tuning setup, and include figures to substantiate your choice of hyperparameters. For example, you could select appropriate metrics and do a grid search with cross validation. Once tuned, include curves corresponding to the best model to the four figures in your blog post, and briefly compare the results to the XGBoost baseline. Include a link to the relevant comet.ml entry for this experiment, and log this model to the model registry.


Accuracy: 0.923

| Actual: No Goal |        60067       |        101        |
|   Actual: Goal  |        4981        |        1241        |
|                 | Predicted: No Goal | Predicted: Goal |


![XGBoost Hyperparameter Tuned](/Images/M2_AM_Q2_XGBoost_Hyper_Tuned.png)

### Comet.ml links:
XGBoost classifier, trained on new features and hyperparameter tuning: [gbdt-hparam-opt](https://www.comet.ml/tim-k-lee/model-registry/gbdt-hparam-opt)




## Q3: XGBoost Trained on Optimal Feature Set


Discuss the feature selection strategies that you tried, and what was the most optimal set of features that you came up with. Include some figures to substantiate your claims. Once you’ve found the optimal set of features via hyperparameter tuning/cross validation, if the feature set is different than what was used for Q2 of this section, include curves corresponding to the best model to the four figures in your blog post, and briefly compare the results to the XGBoost baseline. Include a link to the relevant comet.ml entry for this experiment, and log this model to the model registry.


![XGBoost Optimal](/Images/M2_AM_Q2_XGBoost_Hyper_Optimal.png)

### Comet.ml link:
XGBoost classifier, trained on optimal feature set: [TBD](https://www.comet.ml/tim-k-lee/model-registry/TBD)










