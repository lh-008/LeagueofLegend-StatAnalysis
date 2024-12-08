# LeagueofLegend Analysis: Impact of Rift Herald and Predicting Match Outcomes
By: Longhao Lin, Matthew Wong

# Introduction

League of Legends (LoL) is a widely popular online multiplayer game developed by Riot Games. Among its various game modes, the most iconic one is Summoner's Rift, a 5v5 mode where two teams, blue and red, compete against each other. Each player on the team takes on a unique role, such as a laner (top, mid, bot/ADC, or support) or jungler, each contributing to the team's overall gameplay. While the gameplay can be complex and strategic, the ultimate objective of gameis to destroy opponent's nexus for the victory.

In Summoner's Rift, objectives are one of the most important features of the game. Securing objectives is essential because they provide advantages to the entire team in various ways. For instance, dragons enhance players' stats, taking down turrets grants extra vision and gold, and defeating Baron empowers minions and provides extra gold for the entire team.

For this project, we are particularly interested in understanding the influence of the Rift Herald on in-game statistics. Specifically, our research question is: How does the Rift Herald impact in-game statistics such as gold, experience, and kills in Summoner's Rift matches? To address this question, we will perform exploratory data analysis and use visualizations to discover patterns and identify the Rift Herald's impact in Summoner's Rift.

For this project, we will explore a dataset obtained from Oracle's Elixir. This dataset is comprehensive and offers a variety of features closely tied to the game. For example, it includes data on gold advantages at specific time intervals, the number of objectives a team secured, and the team that ultimately won the match. We will use this dataset to explore our research question.

The dataframe consists of 150,180 rows and 161 columns. However, many of these rows represent individual player statistics within a game. For our analysis, we will filter out these rows, leaving only the rows that represent team-level statistics. We will use the columns defined below for our analysis.

| Column            | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| 'league'          | The name of esport league that match is part of|
| 'gameid'          | The id that belong to the match|
| 'teamkills'       | The total numbers of kills from the team in the match|
| 'teamdeaths'      | The total numbers of deaths from the team in the match|
| 'firstherald'     | A binary value (1 or 0) that indicates whether team secured first rift herald, 1 indicates yes and 0 indicates no|
| 'totalgold'       | The total amount of gold earned by the team|
| 'goldat15'        | The total gold earned by the team at 15 minute|
| 'xpat15'          | The total experience point earned by the team at 15 minute                      |
| 'gamelength'      | The duration of the game in second|
| 'result'          | The outcome of the game in binary value(1 or 0), 1 indicates victory and 0 indicates defeat   |

# Data Cleaning and Exploratory Data Analysis

### Data Cleaning
To make the analysis more efficient and centered around our research question, we will begin with data cleaning.

1. We aim to analyze the impact of the Rift Herald at the team level. Since the dataset includes both individual player and team in-game statistics, we will filter the data to exclude rows corresponding to individual players and keep only those representing team-level statistics.

2. We will drop columns from original dataframe and keep the relevant columns that fit the purpose of our analysis. Specifically, we will use the following columns: `league`, `gameid`, `teamkills`, `teamdeaths`, `firstherald`, `totalgold`, `goldat15`, `xpat15`, `gamelength`, and `result`.

3. The `firstherald` column contains some missing values, which we will filter out to ensure a more accurate and precise analysis.

4. Lastly, we will convert `firstherald` column to type boolean.

The first few rows of the dataframe after cleaning is display below.

| league   | gameid                | position   |   teamkills |   teamdeaths | firstherald   |   totalgold |   goldat15 |   xpat15 |   gamelength |   result |
|:---------|:----------------------|:-----------|------------:|-------------:|:--------------|------------:|-----------:|---------:|-------------:|---------:|
| LCKC     | ESPORTSTMNT01_2690210 | team       |           9 |           19 | True          |       47070 |      24806 |    28001 |         1713 |        0 |
| LCKC     | ESPORTSTMNT01_2690210 | team       |          19 |            9 | False         |       52617 |      24699 |    29618 |         1713 |        1 |
| LCKC     | ESPORTSTMNT01_2690219 | team       |           3 |           16 | True          |       57629 |      23522 |    28848 |         2114 |        0 |
| LCKC     | ESPORTSTMNT01_2690219 | team       |          16 |            3 | False         |       71004 |      25285 |    29754 |         2114 |        1 |
| LCKC     | ESPORTSTMNT01_2690227 | team       |          14 |            5 | False         |       62868 |      24795 |    31342 |         1972 |        1 |

### Univariate Analysis
