---
layout: post
title: NHL Data Science Project - Milestone 2 - Advanced Models
---


# Advanced Models

## Q1: XGBoost Trained on Distance and Angle Features

The XGBoost library was utilized to create the gradient boosted tree classifier, an ensembling method that combines outputs from individual trees to generate the final prediction. A simple XGBoost model with a learning rate of 1, depth of 2, using logistic regression for binary classification was created. This baseline model used the same training/validation setup as the logistic regression models and was trained only on distance and angle features. Compared to the Logistic Regression model trained on distance and angle, the only difference is that the input features were not normalized. This decision was made based on the fact that decision trees are usually not affected by any monotonic transformation. 

The baseline XGBoost model showed a similar problem to its Logistic Regression counterpart: almost no non-zero predictions (i.e. goals) were made. Comparing the performance of the baseline XGBoost and Logistic Regression models in more detail using the classifier quality charts shows marginal improvement in performance by the XGBoost framework (See below). Most notably, the reliability curve shows that the XGBoost model produced predicted probabilities that are inline with the perfectly calibrated line at slightly higher values. 


| Actual: No Goal |        60148       |        20        |
|   Actual: Goal  |        6203        |        19        |
|                 | Predicted: No Goal | Predicted: Goal |


![XGBoost Baseline](/Images/M2_AM_Q2_XGBoost_Baseline.png)

### See Appendix for Comet.ml link.
Experiment entry: https://www.comet.ml/tim-k-lee/ift6758-hockey/70a252e382c74d94ae7b2ff56e3ec7bf




## Q2: XGBoost Trained on New Features and Hyperparameter Tuning

The optimal hyperparameters were obtained through the random search cross validation method. A 5 fold cross-validation splitting strategy was selected, this strategy was repeated 50 iterations to determine the optimal combination. The combination was then refitted one last time using the entire dataset to avoid overfitting. The input features used in this experiment include the new features added in the previous sections but exclude the bonus features.

The parameters obtained through the optimization process are as follow:

| Learning rate step size [learning_rate]            | 0.1 | 
| Number of gradient boosted trees [n_estimators]    | 275 |  
| Maximum tree depth [max_depth]                     | 1 | 
| Minimum loss reduction required for split [gamma]  | 0.1 |

The identified optimal hyperparameters were used to create a tuned XGBoost classifier. The confusion matrix shows that the tuned model predicted more goals than the baseline model and has a minor accuracy increment of ~2%. The two models were plotted on the evaluation figures as shown below. It is very apparent that the tuned model performed better than the baseline. It achieved an AUC of ~0.82, a ~15% increase from the baseline. Both the positive rate by percentile figure and the positive proportion by percentile figure suggest that the probability prediction of the tuned model is more aligned with the actual goal rate. This observation is further reinforced by the reliability curve. The model is capable of generating a high probability prediction even though most of those predictions lie above the perfectly calibrated line rather than overlapping it. Nevertheless, this is the best performing model to this point.

| Actual: No Goal |        60048       |        120        |
|   Actual: Goal  |        5110        |        1112        |
|                 | Predicted: No Goal | Predicted: Goal |

![XGBoost Hyperparameter Tuned](/Images/M2_AM_Q2_XGBoost_Hyper_Tuned.png)

### See Appendix for Comet.ml link.
XGBoost classifier, trained on new features and hyperparameter tuning: [gbdt-hparam-opt](https://www.comet.ml/tim-k-lee/model-registry/gbdt-hparam-opt)




## Q3: XGBoost Trained on Optimal Feature Set

Two methods of performing feature selection were explored, the Lasso and the SHAP. The Lasso method selects features based on penalizing and reducing the corresponding coefficients. The coefficients for insignificant features will eventually be reduced to zero and thus dropped. The SHAP method calculates the impact of each feature to the model and selects features with the highest importance. The list of features that underwent these processes were the features used to determine the optimized hyperparameters in the previous section. 

Both methods generated a very similar result. Out of the 15 input features, 11 features were selected, these features are:  
 - "distance_from_net"
 - "is_rebound"
 - "prev_event_SHOT"
 - "prev_event_time_diff"
 - "angle"
 - "is_empty_net"
 - "shot_Snap Shot"
 - "shot_Slap Shot"
 - "distance_from_prev_event"
 - "coordinate_y"
 - "prev_event_HIT"

The hyperparameter for the model was tuned again using the same optimization process but with the new feature set. The resulting hyperparameters are:

| Learning rate step size [learning_rate]            | 0.062 | 
| Number of gradient boosted trees [n_estimators]    | 495 |  
| Maximum tree depth [max_depth]                     | 5 | 
| Minimum loss reduction required for split [gamma]  | 0.184 |


The results of the tuned model with feature selection were plotted on the classifier quality charts with the previous XGBoost models. The ROC, positive rate by percentile, and positive proportion by percentile all show a comparable result between the hyperparameter optimized model and the models that underwent feature selection. Improvement in performance is observed in the reliability figure. The tuned models trained on the selected features are much closer to the perfectly calibrated line than all other models.

![XGBoost Feature Selected](/Images/M2_AM_Q3_XGBoost_Tuned_Feature_Selected.png)

### See Appendix for Comet.ml link.
XGBoost classifier, trained on optimal feature set: [TBD](https://www.comet.ml/tim-k-lee/model-registry/TBD)









