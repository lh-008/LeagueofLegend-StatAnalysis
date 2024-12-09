# LeagueofLegend Analysis: Impact of Rift Herald and Predicting Match Outcomes
By: Longhao Lin, Matthew Wong

# Introduction

League of Legends (LoL) is a widely popular online multiplayer game developed by Riot Games. Among its various game modes, the most iconic one is Summoner's Rift, a 5v5 mode where two teams, blue and red, compete against each other. Each player on the team takes on a unique role, such as a laner (top, mid, bot/adc, or support) or jungler, each contributing to the team's overall gameplay. While the gameplay can be complex and strategic, the ultimate objective of gameis to destroy opponent's nexus for the victory.

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
| 'xpat15'          | The total experience point earned by the team at 15 minute|
| 'gamelength'      | The duration of the game in second|
| 'result'          | The outcome of the game in binary value(1 or 0), 1 indicates victory and 0 indicates defeat|

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

Let's take a look at the distribution of gamelength from the dataset.

<iframe
  src="assets/distribution_game_length.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The distribution is nearly normal with a slight left skew, reflecting the typical behavior in League of Legends matches. Fewer games end very early or very late, indicating that the data in this dataset is well-suited for analysis.

Let's also take a look at the distribution of total gold from the dataset.

<iframe
  src="assets/distribution_total_gold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The empircal distribution is again, very closely to normal. This distribution represent the normal behavior of league of legends gameplay.

### Bivariate Analysis

Let's take a look at how Rift Herald impact the outcome of the game using the plot below.

<iframe
  src="assets/win_rate_comparison.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The plot shows that teams securing the first Rift Herald have a higher win rate compared to those without it. This suggests that the Rift Herald is an important and impactful objective, significantly influencing the outcome of games. Securing this objective likely provides strategic advantages such as early map control or turret pressure, which leads to higher chance of victory.

Let's also take a look at how Rift Herald impact team gold at 15 minutes.

<iframe
  src="assets/gold15_comparison.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Teams that secure the Rift Herald have a higher total gold at the 15-minute mark compared to those without it. This suggests that the Rift Herald provides an early-game advantage. In a game like League of Legends, such early advantages often 'snowball', growing larger over time and can potentially influencing the outcome of the match.

### Interesting Aggregates

Let’s evaluate the impact of the Rift Herald on the game by analyzing three in-game statistics: `teamdeaths`, `teamkills`, and `totalgold`. We will compare these statistics between teams that secured the first Rift Herald and those that did not across all leagues.

| league     |   ('teamdeaths', False) |   ('teamdeaths', True) |   ('teamkills', False) |   ('teamkills', True) |   ('totalgold', False) |   ('totalgold', True) |
|:-----------|------------------------:|-----------------------:|-----------------------:|----------------------:|-----------------------:|----------------------:|
| CBLOL      |                 15.107  |                13.4198 |                13.3992 |               15.0905 |                57740.3 |               59712   |
| CBLOLA     |                 15.6019 |                13.6019 |                13.5694 |               15.588  |                57484.6 |               59558.9 |
| CDF        |                 19.7368 |                17.3026 |                17.2895 |               19.6842 |                53799.5 |               56666.8 |
| CT         |                 18.3846 |                14.1538 |                14.0769 |               18.2692 |                52747   |               56123.3 |
| DDH        |                 16.4545 |                13.9091 |                13.9043 |               16.4211 |                56432.9 |               59431.5 |
| EBL        |                 16.5081 |                13.7568 |                13.7405 |               16.4486 |                54151.1 |               57519.7 |
| EL         |                 15.7407 |                13.3852 |                13.3481 |               15.7037 |                52756.8 |               55609.5 |
| ESLOL      |                 16.8833 |                14.1667 |                14.125  |               16.8583 |                55420.1 |               58301.3 |
| EUM        |                 15.7978 |                13.8801 |                13.8539 |               15.764  |                54447.9 |               57253.1 |
| GL         |                 17.6264 |                13.546  |                13.5172 |               17.6207 |                54491.5 |               58564   |
| GLL        |                 16.9951 |                14.0739 |                14.0394 |               16.9557 |                54970.1 |               57963.8 |
| HC         |                 15.8889 |                14.3395 |                14.3272 |               15.8519 |                55569.6 |               57476.9 |
| HM         |                 16.0392 |                13.5294 |                13.5033 |               16.0392 |                53896.6 |               57360.8 |
| IC         |                 15.8    |                14.3733 |                14.3333 |               15.7467 |                53068.6 |               55312.2 |
| LAS        |                 16.652  |                14.5022 |                14.4537 |               16.5991 |                53706.4 |               56512.2 |
| LCK        |                 11.8865 |                11.2484 |                11.2334 |               11.8651 |                59105.3 |               60507.5 |
| LCKC       |                 13.3418 |                12.9342 |                12.8937 |               13.3165 |                58443.6 |               59426.3 |
| LCL        |                 12.875  |                 9.75   |                 9.6875 |               12.875  |                50357.5 |               55123.2 |
| LCO        |                 16.3066 |                12.5519 |                12.5094 |               16.283  |                53092.7 |               57099.6 |
| LCS        |                 12.6176 |                11.3922 |                11.3693 |               12.5948 |                57941.5 |               59674   |
| LCSA       |                 15.1241 |                14.0111 |                13.9741 |               15.0944 |                57002.7 |               58735.1 |
| LEC        |                 14.2757 |                12.2675 |                12.2346 |               14.2551 |                58387.5 |               60678.3 |
| LFL        |                 14.3968 |                12.6599 |                12.6316 |               14.3725 |                58775.8 |               61019.7 |
| LFL2       |                 15.0498 |                14.5892 |                14.5726 |               15.0083 |                57125.2 |               58212.2 |
| LHE        |                 15.7992 |                13.7213 |                13.6967 |               15.7746 |                56840.5 |               59218.3 |
| LJL        |                 12.162  |                12.1495 |                12.1389 |               12.1215 |                56741.4 |               57063.7 |
| LJLA       |                 15.5    |                12.3684 |                12.2895 |               15.4474 |                55001.8 |               58655.6 |
| LLA        |                 14.4762 |                12.0703 |                12.0423 |               14.5027 |                57757.2 |               60379.7 |
| LMF        |                 14.0437 |                12.9156 |                12.8938 |               14.0312 |                56969.3 |               58691.3 |
| LPLOL      |                 17.23   |                14.3662 |                14.3333 |               17.2019 |                55269.4 |               58590.5 |
| LVP SL     |                 14.2041 |                12.6449 |                12.6082 |               14.1714 |                57993   |               59979.2 |
| MSI        |                 16.8875 |                11.4375 |                11.425  |               16.8375 |                50348.4 |               56342.1 |
| NEXO       |                 15.9897 |                13.866  |                13.8402 |               15.9639 |                56688.3 |               59473.4 |
| NLC        |                 17.3542 |                13.6198 |                13.5859 |               17.3281 |                54965.4 |               58964.8 |
| PCS        |                 13.7179 |                11.5568 |                11.5348 |               13.6813 |                53641.2 |               56347.8 |
| PGC        |                 18.0798 |                16.4574 |                16.4131 |               18.0301 |                53815.8 |               56028.4 |
| PGN        |                 16.1867 |                13.5333 |                13.5133 |               16.18   |                56965.6 |               59592.2 |
| PRM        |                 15.6774 |                14.6559 |                14.621  |               15.6478 |                56216.2 |               57271.1 |
| SL (LATAM) |                 17.7273 |                14.2909 |                14.2848 |               17.7152 |                55165.2 |               59118.2 |
| TAL        |                 14.1756 |                12.3366 |                12.3122 |               14.122  |                54967.3 |               57544.6 |
| TCL        |                 14.6726 |                12.0493 |                12.0359 |               14.6547 |                55150   |               58439   |
| UL         |                 15.6393 |                12.9098 |                12.8525 |               15.6148 |                56016.3 |               58798.7 |
| UPL        |                 20.7209 |                17.9248 |                17.8835 |               20.682  |                52020.8 |               54927.8 |
| VCS        |                 16.7138 |                14.6369 |                14.6123 |               16.6923 |                54717.1 |               57122.4 |
| VL         |                 16.0824 |                14.0765 |                14.0353 |               16.0353 |                54740.7 |               57376.7 |
| WLDs       |                 14.2128 |                11.695  |                11.6596 |               14.1986 |                55226.5 |               58202.7 |

Teams that secure the first Rift Herald tend to have stronger overall statistics, indicating the important role the Rift Herald plays in influencing the game's progression and outcome.

# Assessment of Missingness

To be filled.

# Hypothesis Testing

To be filled.

# Framing a Prediction Problem

To be filled.

# Baseline Model

To be filled.

# Final Model

To be filled.

# Fairness Analysis

To be filled.