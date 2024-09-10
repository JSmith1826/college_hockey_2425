# College Hockey Analysis 2024-25 Season
### Project Created 8/25/2024 by JBS


## Workbooks

### Team Travel Analysis

This Jupyter notebook calculates the total travel distance for each NCAA college hockey team during the regular season, based on the schedule of games and information about each team's home arena. The goal of this analysis is to assess the travel burden on each team throughout the season, broken down into regional and neutral site games.

#### Files:
- Notebook: *[distance_traveled.ipynb](/workbook/distance_traveled.ipynb)*
- Schedule Information: *[2024_current.csv](/data/schedule/2024_current.csv)*
- On Campus Arena Information: *[arena_school_info.csv](/data/arena_school_info.csv)*
- Neutral Site Arena Information: *[neutral_arenas_2024.csv](/data/neutral_arenas_2024.csv)*

##### This notebook processes two key datasets:
- The 2024 season game schedule, including game dates, teams, and locations.
- Information about each team's home arena, including latitude and longitude coordinates.
- A list of neutral site arenas used for specific games.

#### Steps in the Notebook:
**1. Data Preparation:**

- The notebook begins by loading the game schedule and arena information. It also loads data for neutral site arenas, which are factored into the travel distance calculations.
- Exhibition games are excluded from the dataset to focus only on regular season games.
- Consecutive games at the same site that take place within 3 days (weekend series) are only counted as one trip

**2. Distance Calculation:**

- For each game, the geodesic distance between the home arenas of the competing teams is calculated using the geopy library. For neutral site games, the distance is calculated from each team’s home arena to the neutral venue.
- The total travel distance for each team is computed by summing the distances for all away and neutral site games. Additionally, the average travel distance per game is calculated.

**3. Results:**

The output is a table that includes:
- The total number of trips (both regular and neutral site) each team takes during the season.
- The total distance traveled, broken down into regional and neutral site games.
- The average travel distance per game.
- The closest team to each school (based on geographic proximity) and how many times they play that team during the season.
- The longest trip in each team's schedule including the opponent name and the game type (regular or neutral site)
This information helps quantify the travel demands placed on each team over the course of the season and highlights the additional burden travel places on some teams or conferences.

#### Output:
The [final table](/data/output/Team_Travel_Information_v1.csv) provides a summary of travel statistics for each team:

This table provides a clear overview of each team's travel during the season, broken down into regular and neutral site trips, as well as their proximity to other teams. These insights can help inform discussions on the geographic spread of teams, their travel demands, and potential scheduling efficiencies.
___