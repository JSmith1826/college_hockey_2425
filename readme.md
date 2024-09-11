# College Hockey Analysis 2024-25 Season
### Project Created 8/25/2024 by JBS

## Data Source
All data for this project is come from [CollegeHockeyNews.com](http://https://www.collegehockeynews.com/)

## Workbooks

### Roster Scraping and Cleaning
This Jupyter Notebook performs automated data scraping and cleaning to compile a master roster dataset for all Division 1 college hockey teams for the current season, using CollegeHockeyNews.com as the primary data source.
**Files:**
- **Code:** *[roster_scrape_and_clean.ipynb](/workbook/roster_scrape_and_clean.ipynb)*
- **Output:** *[roster_2024_current_v2.csv](/data/roster_2024_current_v2.csv)*

**1. Data Scraping:**

- The notebook initiates by scraping player roster information from each  team’s page on College Hockey News. This is done by extracting a list of teams from the CHN season schedule and iterating through the team-specific URLs, retrieving roster data, and parsing the HTML content.
- The scraping process extracts all available details from the target page: player names, positions, heights, weights, draft, previous team and hometown information.

**2. Data Cleaning:**

- After scraping, various transformations are applied to standardize the dataset:
    - Columns are cleaned for consistency in naming and formatting.
    -Duplicate or missing data are handled appropriately, ensuring the integrity of the dataset.
    -Team names and associated IDs are correctly matched with the scraped data.

**3. Data Transformation:**

- The hometown information is split into separate columns for City, State/Province, and Country, facilitating detailed geographic analysis.
    - The transformations also include correcting for different formats of hometowns and ensuring all countries are properly labeled.
- Player height is converted from feet and inches to inches for easier analysis.
- The ratio of each class for each class is calculated for later visualization

**4. Data Analysis (Preview):**
- The notebook provides a brief overview of the resulting dataset by displaying distribution summaries:
    - Histograms of height and weight distribution
    - Distribution of player positions
    - Distribution of first and last names
    - Hometown, State/Province and Country distribution

**5. Final Output:**
- The notebook outputs a cleaned and structured master roster table for all teams, ready for further analysis or integration into other projects.

| Current Team   | Last_Name   | First_Name   |   No | Position   | Yr   | Ht   |   Wt | DOB       | Hometown               |   Height_Inches |   Draft_Year |   NHL_Team |   D_Round | Last Team   | League   | City             | State_Province   | Country   |
|:---------------|:------------|:-------------|-----:|:-----------|:-----|:-----|-----:|:----------|:-----------------------|----------------:|-------------:|-----------:|----------:|:------------|:---------|:-----------------|:-----------------|:----------|
| Lake Superior  | Barone      | Adam         |    6 | Defensemen | Fr   | 6-1  |  174 | 5/6/2004  | Sault Ste. Marie, Ont. |              73 |          nan |        nan |       nan | Trail       | BCHL     | Sault Ste. Marie | Ont.             | Canada    |
| Lake Superior  | Blanchett   | Jack         |   16 | Defensemen | So   | 5-11 |  185 | 5/12/2003 | Monroe, Mich.          |              71 |          nan |        nan |       nan | Powell      | BCHL     | Monroe           | Mich.            | USA       |
| Lake Superior  | Brown       | Mike         |    3 | Defensemen | Jr   | 6-2  |  209 | 4/3/2001  | Belmont, Mass.         |              74 |          nan |        nan |       nan | Merrimack   | nan      | Belmont          | Mass.            | USA       |
| Lake Superior  | Bushy       | Evan         |    5 | Defensemen | So   | 6-1  |  195 | 3/26/2002 | Mankato, Minn.         |              73 |          nan |        nan |       nan | Trail       | BCHL     | Mankato          | Minn.            | USA       |
| Lake Superior  | Conrad      | Jacob        |    4 | Defensemen | Fr   | 5-11 |  180 | 5/18/2002 | Green Bay, Wis.        |              71 |          nan |        nan |       nan | Fairbanks   | NAHL     | Green Bay        | Wis.             | USA       |


This tool is a robust foundation for deeper analysis into Division 1 college hockey player demographics, including geographic trends, physical attributes, and more. The clean dataset it produces can easily be integrated into various analysis workflows or visualizations, such as travel or team comparisons.

---

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
    - The result is reported in miles and represent the straight line distance
- The total travel distance for each team is computed by summing the distances for all away and neutral site games. Additionally, the average travel distance per game is calculated.

**3. Results:**

The output is a table that includes:
- The total number of trips (both regular and neutral site) each team takes during the season.
- The total distance traveled, broken down into regular and neutral site games.
- The average travel distance per game.
- The closest team to each school (based on geographic proximity) and how many times they play that team during the season.
- The longest trip in each team's schedule including the opponent name and the game type (regular or neutral site)
This information helps quantify the travel demands placed on each team over the course of the season and highlights the additional burden travel places on some teams or conferences.

#### Output:
| Team              |   Reg_Distance |   Reg_Trips |   Reg_AVG |   N_Distance |   Neutral_Site_Trips |   N_AVG |   Total_Distance |   Overall_AVG | Closest_Team      |   Closest_Distance |   Total_Closest_Matches | Longest_Trip_Opponent   |   Distance_Longest_Trip | Game_Type_Longest_Trip   |
|:------------------|---------------:|------------:|----------:|-------------:|---------------------:|--------:|-----------------:|--------------:|:------------------|-------------------:|------------------------:|:-----------|-----------:|:------------|
| Boston University |        2115.56 |          13 |    162.74 |      2994.6  |                    1 | 2994.6  |          5110.16 |        365.01 | Harvard           |               1.08 |                       1 | Merrimack  |    2994.6  | Neutral     |
| Harvard           |        2750.1  |          17 |    161.77 |      2994.25 |                    1 | 2994.25 |          5744.35 |        319.13 | Boston University |               1.08 |                       1 | Notre Dame |    3606.35 | Neutral     |
| Northeastern      |        2635.15 |          16 |    164.7  |       111.69 |                    1 |  111.69 |          2746.85 |        161.58 | Boston University |               1.76 |                       2 | Denver     |    1768.31 | Regular     |

The [final table](/data/output/Team_Travel_Information_v1.csv) provides a summary of travel statistics for each team:

This table provides a clear overview of each team's travel during the season, broken down into regular and neutral site trips, as well as their proximity to other teams. These insights can help inform discussions on the geographic spread of teams, their travel demands, and potential scheduling efficiencies.
___