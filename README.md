# LeagueofLegend Analysis: Impact of Rift Herald and Predicting Match Outcomes
By: Longhao Lin, Matthew Wong

# Introduction

League of Legends (LoL) is a widely popular online multiplayer game developed by Riot Games. Among its various game modes, the most iconic one is Summoner's Rift, a 5v5 mode where two teams, blue and red, compete against each other. Each player on the team takes on a unique role, such as a laner (top, mid, bot/ADC, or support) or jungler, each contributing to the team's overall gameplay. While the gameplay can be complex and strategic, the ultimate objective of gameis to destroy opponent's nexus for the victory.

In Summoner's Rift, objectives are one of the most important features of the game. Securing objectives is essential because they provide advantages to the entire team in various ways. For instance, dragons enhance players' stats, taking down turrets grants extra vision and gold, and defeating Baron empowers minions and provides extra gold for the entire team. For this project, we are particularly interested in how the Rift Herald influences the game's dynamics and outcomes. We will carry out an EDA to discover patterns and trends that demonstrate how securing Rift Herald can potentially affects team's performance, in-game statistics, and chances of victory.

In this project, we will explore a dataset obtained from Oracle's Elixir. This dataset is comprehensive and offers a variety of features closely tied to the game. For example, it includes data on gold advantages at specific time intervals, the number of objectives a team secured, and the team that ultimately won the match. We will use this dataset to explore our question, that is, how rift herald impact the dynamic and outcome of gameplay.

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

