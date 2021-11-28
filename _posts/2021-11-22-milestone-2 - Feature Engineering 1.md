---
layout: post
title: NHL Data Science Project - Milestone 2 - Feature Engineering 1
---


# Feature Engineering 1

## Q1: Tidied Dataset Visualization

The "Distance from net", "Angle from net", "Is goal", and "Empty Net" information were extracted from the original features. With the final objective of creating a learning model that can predict the probability of a shot to be a goal, these new features were plotted against different shot events to visualize and to gain insights into the dataset. The coordinate of the goal net was approximated with a single point as instructed. 

The graph below shows the relationship between shot events and the distance from the net. The resulting distribution shows that the shot counts were significantly lower outside the attacking/scoring zone. Within the attacking/scoring zone, there was a consistent number of shots distributed at all distances above ~15 ft. It appears that  lower distance to net values corresponds to higher number of goals. The count for both events peaked when the distance from net value was around 9 ft and decreased afterwards. 

![Shot Distribution by Distance from Net](/Images/M2_FE1_Q1_Shot_vs_Distance.png){: .center-image }

The graph below shows the relationship between shot events and the angle from net. A symmetrical distribution of the shot counts with respect to angle from net is observed. A higher distribution of shots is observed at both ~30 and ~-30 degrees. An abnormal number of shot counts is observed at 0 degree. Outside the 30 to -30 degrees angle range, the number of shot counts decreased as the angle increased.

![Shot Distribution by Angle from Net](/Images/M2_FE1_Q1_Shot_vs_Angle.png){: .center-image }

The graph below shows how shots were distributed over both distance and angle from the net. It is noted that the shape of the 2D histogram was governed by the boundary of the ice rink, where larger distance value would correspond to a smaller range of available angles. The graph reveals that the high shot counts region formed a trapezoidal shape distribution (Angle values between ~25 to ~-25 degrees when distance value is ~80 ft, and angle values between 35 and -35 when distance value is ~50 ft). This would correspond to a rectangular shaped high shot counts region within the attacking/scoring zone. It is also noted that there was a high distribution of shots at distance beyond the attacking/scoring zone. The angle and distance would suggest those shots occured in the defending zone.


![Shot Distribution by Distance and Angle from Net](/Images/M2_FE1_Q1_Shot_vs_Distance_Angle.png){: .center-image }


## Q2: Goal Rate Visualization

Plotting goal rate against distance from net and against angle from net reveals additional information on the probability of whether a shot would be a goal.
The graph below shows the relationship between goal rate and the shot distance from the net. The goal rate when the distance from net value is within ~80 ft appears to be reasonable, the probability of scoring was higher when the player was closer to the net. Utilizing information derived from the figures above and under the assumption that the data is correct, the higher goal rate distribution beyond ~80 ft can be attributed to the small sample size of shots from these distances.

![Goal Rate Distribution by Distance from Net](/Images/M2_FE1_Q2_GoalRate_vs_Distance.png){: .center-image }

The graph below shows the relationship between goal rate and the shot angle from net. The graph suggests that the highest goal rate occurred at angles between ~5 to ~10 and between ~-5 to ~-10 degrees. The higher the angle deviation from the center, the lower the goal rate. A dip is observed between ~5 and ~-5 degrees and an abnormal spike is observed at both 0 and ~90 degrees. Using the same assumptions and information as stated above, the anomaly observed at ~90 degrees can be attributed to the lower number of total shots from those angles. The anomaly  observed at 0 degree was the result of assuming the shots taken at zero distance had an angle of 0.

![Goal Rate Distribution by Angle from Net](/Images/M2_FE1_Q2_GoalRate_vs_Angle.png){: .center-image }



## Q3: Sanity Check Using Domain Knowledge

To score a non-empty net goal from the opposite side of the ice rink was incredibly rare. Therefore, any goals that occurred within the defensive zone could be due to mislabelling. The following figures show the relationship between goals and the shot distance from the net and include the information of whether the net was empty or not. 
By plotting the shot counts against distance larger than 80 ft (corresponds to distance outside the attacking/scoring zone), the plots reveal that there were many non-empty net goals, especially between ~160 to ~175 ft.

![Goal Distribution by Distance from Net](/Images/M2_FE1_Q3_Goal_vs_Distance.png){: .center-image }
![Goal Distribution by Distance above 80 ft from Net](/Images/M2_FE1_Q3_Goal_vs_DistanceGreaterThan80.png){: .center-image }

Further investigation revealed that the majority of goals returned by the following query had incorrectly-assigned coordinates

```python
shots[(shots.distance_from_net >= 150) & (shots.is_goal) & (~shots.is_empty_net)]
```

An example of such mislabelled data is Adam Cracknell's first period goal on February 21, 2016, against the Colorado Avalanche.

Reviewing video of the goal available on  [[nhl.com](https://www.nhl.com/video/cracknell-opens-the-scoring/t-278025682/c-41679503)] showed that the shot occurred at the opposite end of the ice from the location implied by the coordinates in the API record, i.e. just a few feet from the net.


![Sample of Mislabelled Data](/Images/M2_FE1_Q3_Mislabelled_Data.png){: .center-image }











