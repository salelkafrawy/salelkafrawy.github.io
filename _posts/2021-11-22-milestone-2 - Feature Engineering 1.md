---
layout: post
title: NHL Data Science Project - Milestone 2 - Feature Engineering 1
---


# Feature Engineering 1

## Q1: Tidied Dataset Visualization

The "Distance from net", "Angle from net", "Is goal", and "Empty Net" information are extracted from the original features. With the final objective of creating a learning model that can predict the probability of a shot to be a goal, these new features are plotted against different shot events to visualize and to gain insights into the dataset. The coordinate of the goal net is approximated with a single point as instructed. 

The graph below shows the relationship between shot events and the distance from net. The resulting distribution shows that the shot counts are significantly lower outside the attacking/scoring zone. Within the attacking/scoring zone, there is a consistant number of shot distributed among at all distances above ~15 ft. The quantity of goal is higher when the distance to net is lower. The count for both events peaked when the distance from net is around 9 ft and decreases afterwards. 

![Shot Distribution by Distance from Net](/Images/M2_FE1_Q1_Shot_vs_Distance.png){: .center-image }

The graph below shows the relationship between shot events and the angle from net. A symmetrical distribution of the shot counts with respect to angle from net is observed. A higher distrbution of shots is observed at both ~30 and ~-30 degrees. An abnormal number of shot counts is observed at 0 degree. Outside the 30 to -30 degrees angle range, the number of shot counts decreases as the angle increases.

![Shot Distribution by Angle from Net](/Images/M2_FE1_Q1_Shot_vs_Angle.png){: .center-image }

The graph below shows the correlation between the shot distribution and both distance and angle from net. It is noted that the shape of the 2D histogram is goverened by the boundary of the ice rink, where larger distance value would correspond to a smaller range of available angles. The graph reveals that high shot counts region forms a trapezoidal shape distribution (Angle between ~25 to ~-25 degrees when distance is ~80 ft, and angle between 35 and -35 when distance is ~50 ft). This would correspond to a rectangular shape high shot counts region within the attacking/scoring zone. It is also noted that there is a high distribution of shots at distance beyond the attacking/scoring zone. The angle and distance would suggests those shots occured in the defending zone.


![Shot Distribution by Distance and Angle from Net](/Images/M2_FE1_Q1_Shot_vs_Distance_Angle.png){: .center-image }


## Q2: Goal Rate Visualization

Plotting goal rate against distance from net and against angle from net reveals additional information on the probability of whether a shot would be a goal.
The graph below shows the relationship between goal rate and the shot distance from net. The goal rate when the distance from net is within ~80 ft appears to be reasonable, the probability of socring is higher when the player is closer to the net. Utilizing the information derived from the figures above and under the assumption that the data is correct, the higher goal rate distribution beyong ~80 ft can be attributed to the low number total shots from those regions.

![Goal Rate Distribution by Distance from Net](/Images/M2_FE1_Q2_GoalRate_vs_Distance.png){: .center-image }

The graph below shows the relationship between goal rate and the shot angle from net. The graph suggests that the highest goal rate occurs at angles between ~5 to ~10 and between ~-5 to ~-10 degrees. The higher the angle deviation from the center, the lower the goal rate. A dip is observed between ~5 and ~-5 degrees and an abnormal spike is observed at both 0 and ~90 degrees. Using the same assumptions and information as stated above, this anomally observed at ~90 degrees can be attributed to the lower number of total shots from those angles. The anomally observed at 0 degree would be a feature of the dataset.

![Goal Rate Distribution by Angle from Net](/Images/M2_FE1_Q2_GoalRate_vs_Angle.png){: .center-image }



## Q3: Sanity Check Using Domain Knowledge

Domain knowledge suggests that it would be incredibly rare to score a non-empty net goal on the opposing team from within one's defensive zone. Therefore, any goal event that occured at a distance that corresponds to the defensive zone should be examined. The following figures shows the relationship between goal event and the shot distance from net, it also shows the information of whether the net is empty of non-empty. 
By plotting the shot counts against distance larger than 80 ft (corresponds to distance outside the attacking/scoring zone), it is revealed that there many non-empty net goals, especailly between ~160 to ~175 ft.

![Goal Distribution by Distance from Net](/Images/M2_FE1_Q3_Goal_vs_Distance.png){: .center-image }
![Goal Distribution by Distance above 80 ft from Net](/Images/M2_FE1_Q3_Goal_vs_DistanceGreaterThan80.png){: .center-image }

Further investigation reveals that the majority of the goal information returned by the following query are mislabeled.

```python
shots[(shots.distance_from_net >= 150) & (shots.is_goal) & (~shots.is_empty_net)]
```

An example of such mislabelled data is Adam Cracknell's first period goal on February 21, 2016, against the Colorado Avalanche.

It is labeled with a x_coordinate value (see figure below) much higher than reality. The data suggests that the shot occured at the opposite end of the specturm, rather than within a few feet from the goal net. [[nhl.com](https://www.nhl.com/video/cracknell-opens-the-scoring/t-278025682/c-41679503)]

![Sample of Mislabelled Data](/Images/M2_FE1_Q3_Mislabelled_Data.png){: .center-image }











