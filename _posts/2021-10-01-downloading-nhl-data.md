---
layout: post
title: Downloading NHL Game Data with the NHL API
---

The [NHL Stats API](http://statsapi.web.nhl.com/) is a rich source of historical hockey data.

In this tutorial, we will show you how to download gameplay data from the NHL API programmatically.


## Understand
The NHL gameplay data is organized primarily by the starting year of each season (2016, 2017, etc.), then subseason (preseason, regular season, playoffs, and all-star games).

This information is combined with game-level enumeration conventions to assigned each game a unique ID. For more detail on how numeric codes map to the organization of the API, see the [unofficial NHL Stats API documentation](https://gitlab.com/dword4/nhlapi/-/blob/master/stats-api.md#game-ids).


## Implement
We begin by writing a simple function to get a `game_url` from a `game_id` as determined by the API's naming conventions:

```python
def get_game_url(game_id: str):
    """ Returns an NHL stats API URL based on an NHL GAME_ID """
    return f"https://statsapi.web.nhl.com/api/v1/game/{game_id}/feed/live/"
```

We then write a function which retrieves data from an API url for a list of game IDs. Since the NHL API is HTTP-based, we will use python's standard `requests` library:

```python
def download_games(game_ids: List, datadir: os.PathLike):
    """ Downloads data for a set of NHL Game IDs.

        Applies a data directory structure of year/type/ID.json
        Logs warnings if no data associated with game_id.
    """
    for game_id in game_ids:
        response = requests.get(get_game_url(game_id))

        if response.status_code == 404:
            pass  # handle errors as desired, but likely corresponds to a playoff game that wasn't necessary
        else:
            subseason = "regular" if game_id[4:6] == "02" \
                          else "postseason" if game_id[4:6] == "03" \
                          else None
            if not subseason:
                raise ValueError(f"{game_id[4:6]} is not a recognized subseason code")

            path_to_datafile = os.path.join(datadir, game_id[:4], subseason, f"{game_id}.json")
            with open(path_to_datafile, "wb") as f:
                f.write(response.content)
```

Finally, we write a function to construct actual game ids for seasons of interest:

```python
def generate_regular_season_game_ids(season: int):
    """ For an NHL season starting in year SEASON, return all regular season game IDs.
    """
    regular_season_games = 1230 if season <= 2016 else 1271

    regular_game_ids = []
    for game_num in range(1, regular_season_games+1):
        game_num_padded = str(game_num).zfill(4)
        regular_game_id = str(season) + "02" + game_num_padded
        regular_game_ids.append(regular_game_id)

    return regular_game_ids
```

Implementation of `generate_postseason_game_ids` is left as an exercise.

Putting things together, we call our functions in a script:

```python
for season in seasons:
    requested_game_ids = []
    requested_game_ids.extend(generate_regular_season_game_ids(season))
    requested_game_ids.extend(generate_postseason_game_ids(season))

    download_games(requested_game_ids, args.datadir)
```
