---
layout: post
title: NHL Data Science Project - Milestone 2 - Give It Your Best Shot!
---


# Give It Your Best Shot!

## Q1: Explored Models Discussion and Comparison




Neural networks was one of the techniques explored to create a better goal probability prediction model. Four different MLP models were created using different input feature sets, the feature set and the included features were:
- Distance: `distance_from_net`
- Baseline: `distance_from_net`, `angle`
- Basic: `period`, `goals_home`, `goals_away`, `shooter_id`, `coordinate_x`, `coordinate_y`, `distance_from_net`, `angle`
- Advance: `game_sec`, `period`, `secondary_type`, `coordinate_x`, `coordinate_y`, `distance_from_net`, `angle`, `prev_event_type`, `angle_between_prev_event`, `distance_from_prev_event`, `prev_event_time_diff`, `speed`, `is_rebound`, `rebound_angle`, `is_empty_net`

All the feature set were preprocessed using the following procedure:
- Consolidate the representation of certain categorical features by relabeling different events with the same label.
- Encode categorical features using one-hot encoding.
- Normalize all features by subtracting the feature mean and scaling to unit variance.
- Replace all NaN values with 0.
   
The MLP models used the Adam optimization algorithm with a logistic activation function and adaptive learning rate. The number of neurons in the input layer was selected to be the number of input features plus one, similarly the output layer had one output neuron for the binary class plus one additional neuron. The one extra neuron was intended to represent the bias term. Only a single hidden layer was used, the number of hidden neurons was the mean of the input neurons and the output neurons.
 
The MLP models trained on the distance, baseline, and basic feature set produced the same accuracy of ~90 % and the same confusion matrix with zero prediction of goals. The MLP model trained on the advance feature set produced an accuracy of ~92 % and the prediction of goals was non-zero as shown in the confusion matrix below.

| Actual: No Goal |        60113       |        55        |
|   Actual: Goal  |        5023        |        1199        |
|                 | Predicted: No Goal | Predicted: Goal |

Evaluating the models using the classifier quality charts suggests that the performance of the model increases as the number of input features increases as shown below. The model trained on the advance feature set outperformed all other models. The increase in AUC using the distance feature set and the advance feature set was close to 20 %. The reliability curve shows that using the advance feature set allowed the model to become more aligned with the perfectly calibrated line. The true positive rate curve shows a significant performance improvement at high probability percentiles when using the advance feature set.
 

![Neural Network Models Comparison](/Images/M2_BS_Q1_NeuralNetworkComparison.png)

The effect of the number of hidden layer neurons was investigated and the results plotted in the evaluation figures shown below. The model trained on the advance feature set was used in this exercise. The figures suggest that the number of hidden neurons had no direct impact on the performance of the model.

![Neural Network Models Comparison](/Images/M2_BS_Q1_HiddenNeuronComparison.png)






![Model Comparison](/Images/M2_BS_Q1_ModelComparison.png)

### Comet.ml links:
Experiment entry:
TBD Model: [TBD](TBD)








