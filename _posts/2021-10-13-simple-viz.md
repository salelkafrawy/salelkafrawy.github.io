---
layout: post
title: Simple Visualization
---

## Q1

![Shot distributions by type, 2018 season](/Images/shot-distribution-by-type.png)


|Shot Type |Goals|Shots (excluding Goals) |Goal Percentage|
|:------------:|:--:|:---:|:---:|
|Tip-In        |761 |3547 |0.177|
|Deflected     |263 |1286 |0.170|
|Backhand      |741 |5803 |0.113|
|Snap Shot     |1155|10406|0.100|
|Wrist Shot    |3854|39999|0.089|
|Wrap-around   |60  |824  |0.068|
|Slap Shot     |768 |10955|0.066|


Shot-level data from the 2018-19 season makes it clear that tips (intentional redirections of one player's shot by another player) and deflections (unintentional redirections) are very dangerous situations for defending teams.

As expected, snap and wrist shots are the most common shot types. This makes sense because both types can be easily disguised from defending goaltenders: snap shots require no prior adjustment of the player's hold on the stick, while wrist shots look similar to passes until the moment they are released.


## Q2

![Goal percentage by distance, 2018-2020](/Images/goal-percentage-by-distance.png)
_Note:  Excludes shootouts, empty net situations, and shots from outside the offensive zone_

Goal percentages by distance from the net for recent seasons show that shots taken close to the net convert to goals at a consistently higher rate, from almost 40% within 5 feet of the net to roughly 2.5% near the blueline at 70 feet.

There is no significant variations between seasons.

It is worth cautioning that this association is highly unlikely to be causal -- shots taken close to the net are probably consequences of superior talent and planning (or just luck) on the side of the offensive team.


## Q3
![Goal percentage by shot type, 2018-2020](/Images/goal-percentage-by-shot-type.png)
_Note: Excludes shootouts, empty net situations, and shots from outside the offensive zone_

Breaking down goal percentages by shot type, we see that our conclusion about the power of tip-ins and deflections is moderated by their prevalance at extremely short distances.

Instead, close-range slap shots convert at consistently higher rates than than snap and wrist shots taken at similar distances.

Again, these statistical associations do not imply causality. For example, while slap shots are more dangerous than snap shots, it is not always possible for a player to setup for a slap shot. Therefore, assuming teams are attempting to maximize expected goals per game, taking many snap shots may actually be preferable to setting up relatively fewer slap shots.

The comments above are reinforced by a breakdown of shot attempts by type over distance:


![Shot attempts by distance and type, 2018-2020](/Images/shot-attempts-by-type.png)
_Note: Excludes shootouts, empty net situations, and shots from outside the offensive zone_
