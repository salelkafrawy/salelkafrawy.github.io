---
layout: post
title: Feature Engineering 2
---

# New Features Description
The newly added features with a brief description are as follows:
- Game period: (`period`: at which period of the game the event was recorded in)
- Shot distance: (`distance_from_net`: distance between the shot and the net)
- Shot angle: (`angle`: the angle with respect to the net where the shot happened)
- Shot type: (`type`: shot main type)
- Shot secondary type: (`secondary_type`: shot secondary type)
- Empty net: (`is_empty_net`: a binary variable whether the net was empty or not)
- Coordinates of the last event: (`coordinate_x`, `coordinate_y`, are the seperate columns for the x and y coordinates respectively)
- Game seconds: (`game_sec`: Total number of seconds elapsed in the game)

Information from the immediately preceding event as four new features:
- Last event type: (`prev_event_type`: the type of the preceding event)
- Coordinates of the last event (`prev_event_x_coord`, `prev_event_y_coord`: x and y coordinates for the previous event)
- Time from the last event (seconds): (`prev_event_time_diff`: the difference between current event and the preceding event in seconds)
- Distance from the last event: (`distance_from_prev_event`: the distance between current event and the preceding one)

Additional features that quantify the state of the play:
- Rebound (bool): (`is_rebound`: a binary column that is true if the current and preceding events were shots, otherwise false)
- Change in shot angle (`rebound_angle`: only included if the shot is a rebound, otherwise 0. It is the angle between both shots)
- Speed:  (`speed`: defined as the distance from the previous event, divided by the time since the previous event)

The saved dataframe with the previous features of the game id=2017021065 (Winnipeg vs Washington game on March 12, 2018) is stored in [this comet.ml experiment](https://www.comet.ml/tim-k-lee/ift6758-hockey/1044dea36bb240f785c459c045f91b50) under the saved artifacts. 