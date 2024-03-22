# League of Legends Early Game Analysis
By David Tsukamoto

# Introduction
League of Legends is a game that was created in 2009 that has only continued to grow in popularity over the years. With the growth of the game came a competitive scene, esports. The dataset that we use in this project is taken from pro games in 2022 which has about 15,000 rows of data. 

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


<iframe
  src="assets/killdist1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

________

<iframe
  src="assets/leaguedist2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

_______
<iframe
  src="assets/ladist3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______
<iframe
  src="assets/lkdist4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______
<iframe
  src="assets/empdist5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______
<iframe
  src="assets/empdist6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
_______
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