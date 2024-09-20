# College Hockey Analysis 2024-25 Season
### Project Created 8/25/2024 by JBS

## Data Source
Data for this project is collected ptimarily from [CollegeHockeyNews.com](http://https://www.collegehockeynews.com/). [The Rink Live's](https://www.therinklive.com/) Transfer Portal Tracker is also used

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
### Team Composition Analysis by Class Rank and Age

**Files:**
- **Code:** *[age_experience_plots.ipynb](/workbook/age_experience_plots.ipynb)*

This notebook is designed to analyze and visualize the makeup of college hockey teams by class rank (Freshman, Sophomore, Junior, Senior, Graduate) and average age. Using team roster data, it performs data transformation to aggregate the proportions of each class rank per team, along with the team's average age.

**Key Features:**
- **Data Transformation:** The notebook processes team roster data and calculates the proportion of players in each class rank, as well as the team's average age. The final transformed data can be adapted to analyze different conferences or groups of teams.

- **Dynamic Plotting Function:** A core feature of this notebook is a customizable function that generates stacked bar charts representing the class rank distribution for each team in a given conference. The function is adaptable, allowing you to switch between different conferences with minimal adjustments to the input data.

- **Visual Insights:** The stacked bar charts provide clear visual insights into how teams are composed across different experience levels (class ranks) and can help identify trends such as team reliance on younger or older players.

**Usage:**
To adapt this notebook for another conference or group of teams, simply adjust the input dataset to reflect the teams and roster information of interest. The plotting function will automatically update to reflect the new data.

This notebook can be extended to support a variety of visualization needs within the context of college hockey analytics, making it a versatile tool for exploring team composition and player experience.

#### **Example of output images:**
![By Conference Plot](/images/readme_images/all_conferences_comparison.png)
![Big Ten Plot - 2024 Season](/images/readme_images/Big%20Ten_age_experience_plot.png)
![Hockey East Plot - 2024 Season](/images/readme_images/Hockey%20East_age_experience_plot.png)

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

### Mapping Workbook

#### Files:
**Notebook**: [mapping_workbook.ipynb](/workbook/mapping_workbook.ipynb)
**Geography (Shapefile)**: [Census.gov Cartographic Boundary Files](https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html)
**School Information**: [arena_school_info.csv](/data/arena_school_info.csv)



### Key Steps:
**Data Loading:**

- Imports shapefiles for U.S. states and counties using GeoPandas.
- Loads a CSV file containing school details, such as locations, team colors, and logo paths.

**Data Transformation:**

- Transforms the school information into a Python dictionary, making it easy to access and reference coordinates, colors, and logos throughout the code.

**Map Creation:**

- Initializes a Folium map centered on the U.S.
- Adds custom markers for each school, using logos that can be scaled based on a "zone factor" (relative influence of each team).
- Colors counties based on the closest team's official colors by applying geoJSON layers.
- Includes interactive tooltips that display the name of the closest team when hovering over a county.
Output:

The final map is saved as an HTML file, making it accessible outside the notebook for easy sharing and viewing.

**Libraries Used:**
- Folium: For creating interactive maps with layers, tooltips, and custom icons.
- GeoPandas: For reading and managing geographic shapefiles, including state and county boundaries.
- Pandas: For handling the school information data.
- PIL (Python Imaging Library): To manage image data, such as team logos.

**Adaptability:**
The code is highly customizable: users can adjust the map's base style, modify icon sizes, or easily swap data inputs like team locations or regions. This flexibility allows it to be reused for various geographic or sports visualizations.

***Output screenshot:***
![US Map](/images/export/closest_team_cont_us.png)
![Northeast](/images/export/closest_team_northeast.png)


---