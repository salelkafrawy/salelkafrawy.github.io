---
layout: post
title: Feature Engineering 2
---

# New Features Description
The newly added features with a brief description are as follows:
- **Game period** (int) [`period`]: Period of the game the event was recorded in.
- **Shot distance** (float) [`distance_from_net`]: Distance between the shot and the net.
- **Shot angle** (float) [`angle`]: The angle with respect to the net where the shot happened.
- **Shot type** (str) [`type`]: The primary shot event label.
- **Shot secondary type** (str) [`secondary_type`]: The secondary shot event label.
- **Empty net** (bool) [`is_empty_net`]: A binary variable whether the net was empty or not.
- **Coordinates of the current event** (int) [`coordinate_x`, `coordinate_y`]: Two seperate columns for the x and y coordinates of the event respectively.
- **Game seconds** (int) [`game_sec`]: Total number of seconds elapsed in the game.

Using information from the immediately preceding event as four new features:
- **Last event type** (str) [`prev_event_type`]: The preceding event's event type.
- **Coordinates of the last event** (int) [`prev_event_x_coord`, `prev_event_y_coord`]: X and Y coordinates for the previous event.
- **Time from the last event** (int) [`prev_event_time_diff`]: The difference between current event and the preceding event in seconds.
- **Distance from the last event** (float) [`distance_from_prev_event`]: The distance between current event and the preceding one.

Additional features that quantify the state of the play:
- **Rebound** (bool) [`is_rebound`]: A binary column that is true if the current and preceding events were shots, otherwise false.
- **Change in shot angle** (float) [`rebound_angle`]: Only included if the shot is a rebound, otherwise 0. It is the angle between both shots.
- **Speed** (float) [`speed`]: Defined as the distance from the previous event, divided by the time since the previous event.


{% comment %}
Bonus features to capture the power-play situation:
- **Home team power play timer** (int) [`PowerPlayTimerHome`] : The timer that indicates the duration of the power play for the home team.
- **Guest team power play timer** (int) [`PowerPlayTimerGuest`] : The timer that indicates the duration of the power play for the guest team.
- **Home team skater number** (int) [`Home_Skaters`] : Number of home team non-goalie skaters, no less than 3.
- **Guest team skater number** (int) [`Guest_Skaters`] : Number of guest non-goalie team skaters, no less than 3.
{% endcomment %}


The saved data frame with the above features of the game id=2017021065 (Winnipeg vs Washington game on March 12, 2018) was stored in [this comet.ml experiment](https://www.comet.ml/tim-k-lee/ift6758-hockey/1044dea36bb240f785c459c045f91b50) in the dataframes folder under Assets & Artifacts. 