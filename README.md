# League of Legends Early Game Analysis
By David Tsukamoto

# Introduction
League of Legends is a game that was created in 2009 that has only continued to grow in popularity over the years. With the growth of the game came a competitive scene, esports. With esports, has come lots of data that we are able to use to find trends or answer questions. The dataset that we use in this project is taken from pro games in 2022 which has about 15,000 rows of data. 

The question I wanted to ask was "Among Tier-one professional leagues, which league has the most aggressive early game?" The reason I wanted to ask this question was to understand if all pro leagues had the level of aggresion in the early game due to the risk that comes with high aggression. If pro players don't see aggression in the early game as important, should we also think of the early game as a simple farming phase? Following the course of this question, I plan on using the following columns in my analysis.

| Column      | Description |
| ----------- | ----------- |
| `league` | The league the game was played in |
| `datacompleteness`|The state of the data in the row |
| `killsat15` | The number of kills the team had at 15 minutes |
| `opp_killsat15`| The number of kills the other team had at 15 minutes |
| `assistsat15`  | The number of assists the team had at 15 minutes |
| `opp_assistsat15` | The number of assists the other team had at 15 minutes |
| `patch` | The patch that the game was played in |
| `firstherald` | 1 if the team got the first dragon, 0 if they didn't |
| `firstblood` | 1 if the team got the first kill, 0 if they didn't |
| `firsttower` | 1 if the team got the first tower, 0 if they didn't |
| `split` | The part of the season which the game was played|

# Data Cleaning and Exploratory Data Analysis

The first thing that I did was remove rows that didn't have the data that I needed and replaced them with other rows that already existed in the dataset. I had to replace the entire row because if I didn't, the data that would replace it would mess up my prediction dataframe which hinged on how each of the features predict an outcome. To get the values I used probabilistic imputation to impute the missing values.  I also decided that I was going to create 2 different dataframes, 1 for hypothesis testing and the other for prediction. 

For my hypothesis dataframe, I created 2 new variables`'allkillsat15`,`allassistsat15`, which were created by combining the columns `killsat15`, `opp_killsat15`,`assistsat15`, and `opp_assistsat15`. 
The dataframe looks like this:

| league   |   allkillsat15 |   allassistsat15 |
|:---------|---------------:|-----------------:|
| LCK      |              6 |               10 |
| LCK      |              4 |                3 |
| LCK      |              9 |               14 |
| LCK      |              2 |                3 |
| LCK      |             11 |               18 |

For my prediction dataframe, I also used the columns `'allkillsat15`,`allassistsat15` along with many other columns that will help me in the prediction problem
This data frame looks like this:

|   patch |   result |   firstdragon |   firstherald |   firstblood |   firsttower | split   |   csdiffat15 |   killdiffat15 |   assistdiffat15 |
|--------:|---------:|--------------:|--------------:|-------------:|-------------:|:--------|-------------:|---------------:|-----------------:|
|   12.01 |        0 |             0 |             1 |            1 |            1 | Spring  |          -23 |             -1 |               -8 |
|   12.01 |        0 |             0 |             1 |            0 |            0 | Spring  |          -22 |             -2 |               -2 |
|   12.01 |        1 |             1 |             0 |            0 |            1 | Spring  |           15 |              2 |                7 |
|   12.01 |        1 |             1 |             0 |            0 |            1 | Spring  |           15 |              2 |                7 |
|   12.01 |        0 |             0 |             1 |            1 |            1 | Spring  |          -40 |              2 |                6 |

## Univariate Analysis:

In Univariate Analysis we will analyze the distribution of Kills at 15 minutes.

### Distribution of Kills at 15 Minutes

Here we see that our distribution is a positive skew that centers around 7 kills. This data is pretty surprising since pro players tend to play a slow and safe early game to reduce risky plays.

<iframe
  src="assets/killdist1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Bivariate Analysis:

In Bivariate Analysis we will analyze the distribution of Kills at 15 minutes across Leagues.

### Distribution of Kills at 15 minutes by League

Below we can see that VCS league has a box plot that his much higher compared to the other leagues.

<iframe
  src="assets/lkdist4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

Here we look at the means of each league and we can see that the VCS again has very

| league   |   allkillsat15 |   allassistsat15 |
|:---------|---------------:|-----------------:|
| VCS      |       10.4118  |         15.5108  |
| CBLOL    |        7.42798 |         13.2181  |
| PCS      |        6.97048 |         12.2472  |
| LPL      |        6.76845 |         11.388   |
| LLA      |        6.68984 |         11.5615  |
| LEC      |        6.19403 |         10.4876  |
| LCS      |        5.76645 |          9.77303 |
| LCK      |        5.57173 |          9.71734 |

#Assessment of Missingness

## NMAR
I believe that there is a column in the dataset that is NMAR, which is `dragons (type unknown)`. This column tends to have missing data, but you cannot infer it's data from other columns so it cannot be missing by design. This column exists for the premise that the data is somwhat missing so it's really the value of the column itself that is the reason for its missingness.

## Missingness Dependency
I noticed while looking through the data that there were a lot of values missing at the end of the dataset, specifically the data related to 15 or 10 minutes like what we are using.
I also found that there were a lot of missing values in certain leagues so I wanted to see if this was really true.

So I want to see if the missingness of `killsat15` depends on `league` among tier 1 professional leagues. Below we see the proportions of where the data of `killsat15` are missing in comparison to `league`. We can see that all the missing values are in the LPL, while the LPL also has no non-missing values.

| league   |   is_missing = False |   is_missing = True |
|:---------|---------------------:|--------------------:|
| CBLOL    |            0.121743  |                   0 |
| LCK      |            0.233968  |                   0 |
| LCS      |            0.152305  |                   0 |
| LEC      |            0.100701  |                   0 |
| LLA      |            0.0936874 |                   0 |
| LPL      |            0         |                   1 |
| PCS      |            0.135772  |                   0 |
| VCS      |            0.161824  |                   0 |

### Null hypothesis: The distribution of `league` when `killsat15` is missing is the same as the distribution of the `league` when `killsat15` is not missing 

### Alternative hypothesis: The distribution of the `league` when `killsat15` is missing is different from the distribution of the `league` when `killsat15` is not missing

Below we can see that our observed TVD is much higher than the TVDs we gathered through permutation, so it is reasonable to say that we reject our null hypothesis and say that the missing ness of `killsat15` is MAR since it's missingess is correlated with `league`

<iframe
  src="assets/empdist5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______

Now we want to see if the `result` of a match has some correlation with the missingness of `killsat15`.

Below we see that the values are pretty balanced, however we see slightly higher values when the team wins the game compared to a loss.

|   result |   is_missing = False |   is_missing = True |
|---------:|---------------------:|--------------------:|
|        loss |             0.476954 |            0.450382 |
|        win |             0.523046 |            0.549618 |

### Null hypothesis: The distribution of `result` when `killsat15` is missing is the same as the distribution of the `league` when `killsat15` is not missing 

### Alternative hypothesis: The distribution of the `result` when `killsat15` is missing is different from the distribution of the `league` when `killsat15` is not missing

In the graph below, we can see that our observed TVD isn't significant, so we would fail to reject our null hypothesis and say that `killsat15` is MCAR because it's missingness is not correlated with `result` 

<iframe
  src="assets/empdist6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing

<iframe
  src="assets/hypo7.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______
<iframe
  src="assets/dist8.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>