# League of Legends Monster Kills vs Win Rates
DSC80 Project at UCSD about data analysis on tournament data from League of Legends.

The purpose of this project is to conduct analysis on League of Legends tournament data in order to extract valuable data regarding optimal strategies that can be taken to increase the odds of winning more games.

Author: Yadushan Thillainathan

## Introduction:
League of Legends is a popular game in the MOBA genre that amassed an extremely large player base and has made strides in the world of esports as it is one of the forefronts of tournament play for video games in the modern age. The dataset that is covered in this project is comprised of tournament data from the League of Legends world championship in 2022. The dataset in questions covers a wide variety of data including information regarding the team (eg character picks, character bans, etc.), player performance data (eg kills, deaths, assists, etc.), and match data (monsters killed, gold accumulated, etc.). It has 161 columns and 150588 rows. 

In the world of comeptitive gaming, any advantage gained over the other team is a means for victory. This includes strategy. The team with the best strategy will naturally win the most games. For the purposes of this project, I decided to focus my efforts into the match data. In the game, players must balance their gameplay between fighting for the main objective, slaying enemy players, and accumulating resources. A large part of this is defeating monsters and minions in order to accumulate gold and experience point so that fighting against players and enemy towers becomes a much easier task. 

The central question this project is focused around is: do teams who kill more monsters win more games? This question will be answered by conducting data analysis on the dataset to see if any trends appear between wins and monster kills and then using this information to make a predictive model that might be able to determine if a team will win based on this data.

### Columns:
The dataset contains a very extensive array of data to analyze, but for the purpose of this project, the one that we will focus on are as follows.

'monsterkills': This column consists of the amount of monsters that were killed by each player and team
'totalgold': This column includes the amount of gold that each player and team accumulated throughout the match
'kills': This column includes the amount of kills on enemy players that each player and team accumulated throughout the match
'minionkills': This column includes the amount of kills on enemy minions that each player and team accumulated throughout the match
'deaths': This column includes the amount of deaths that each player and team accumulated throughout the match
'assists': This column includes the amount of assists on enemy minions that each player and team accumulated throughout the match
'goldspent': This column includes the amount of gold that each player and team spent throughout the match
'gamelength': This column includes the length of the game's duration

## Data Cleaning and Exploratory Data Analysis:
### Data Cleaning:
The first step of the data cleaning process is to drop all of the data regarding individual players. For the purposes of this project is to analyze team performance, not individual. This data set has rows for players followed by rows of data from teams, so we will only keep this team data. Then, not all rows are complete and this is shown by the datacompleteness column which tells if the row is complete or not. All rows that are not complete are droppped. Finally, only the relevant columns that I will be tested are kept.

|    |   monsterkills |   minionkills |   totalgold |   goldspent |   kills |   deaths |   assists |   gamelength |
|---:|---------------:|--------------:|------------:|------------:|--------:|---------:|----------:|-------------:|
| 10 |            160 |           680 |       47070 |       44570 |       9 |       19 |        19 |         1713 |
| 11 |            184 |           792 |       52617 |       45850 |      19 |        9 |        62 |         1713 |
| 22 |            215 |           994 |       57629 |       53945 |       3 |       16 |         7 |         2114 |
| 23 |            244 |          1013 |       71004 |       66410 |      16 |        3 |        39 |         2114 |
| 46 |            269 |           874 |       62868 |       57615 |      14 |        5 |        42 |         1972 |

### Univariate Analysis:
The graph below shows the distribution of monster kills for teams that won. It appears to be relatively normal in its distribution.

<iframe
  src="assets/univariate_win_only.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The graph below shows the distribution of monster kills for teams that lost. It also appears to be relatively normal in its distribution.

<iframe
  src="assets/univariate_loss_only.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

When overlaying these graphs over one another we can see that teams that won did tend to have more monster kills on average than teams that lost.

<iframe
  src="assets/shared_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Based on these graphs it seems that teams that are winning do seem to kill more monsters. However, further analysis will need to be done in order to prove this.

### Bivariate Analysis:
I graphed the percentage of teams that had more monster kills than the other by whether they won or lost. This graph shows that teams that had more monster kills definitely won more often than they lost. This seems to support the fact that monster kills have a positive relationship with win rates. 

<iframe
  src="assets/bivariate_monster.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates:
When grouping by the result, we can find some very interesting aggregates. This shows that teams that won had more monster kills, more minion kills, more kills, more assists, more gold accumulated, less deaths, and shorter games.

|   result |   monsterkills |   minionkills |   totalgold |   goldspent |   kills |   deaths |   assists |   gamelength |
|---------:|---------------:|--------------:|------------:|------------:|--------:|---------:|----------:|-------------:|
|        0 |    1.96589e+06 |   8.60329e+06 | 5.65829e+08 | 5.45821e+08 |  103248 |   215430 |    220200 |  2.23322e+07 |
|        1 |    2.3337e+06  |   8.78299e+06 | 6.70219e+08 | 6.00522e+08 |  213393 |   103088 |    482983 |  2.17028e+07 |

## Assessment of Missingness:
### NMAR Analysis
When looking at the data it appears that soeme of the incomplete data have missing values for some of the kill streaks, such as double kills, triple kills, etc. I don't believe that these are NMAR (not missing at random) because at the highest level of play, it might be hard to defeat multiple top players in a row, which is why kill streaks become a difficult task. As such, these values may be missing because its likely that they may never happen in a game at the competitive level. Since, the missingness of the data depends on itself, it makes sense that this would be NMAR. In order to make it MAR (missing at random), some additional data may be needed. For example, a column that states if any killstreaks occured during the game may result in the missingness of this killstreak data dependent on whether or not the anykillstreaks column is true or false.

### Missingness Dependency
Other columns also experience some missing values. I first started by testing the missingness of double kills based on first bloods.

Null Hypothesis: The missingness of the doublekills column is independent of the firstblood column
Alternate Hypothesis: The missingness of the doublekills column depends on the firstblood column

After performing a permuatation test, the resulting value is extremely small because of the observed difference being so much greater than the distribution. Because our p-value is less than 0.05, we can reject the null and determine that this is a significant result and that double kills being missing is dependent on first bloods.

<iframe
  src="assets/missingness_firstblood.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I also check the missingness of bans based on the result column.

Null Hypothesis: The distribution of result is independent of whether ban1 is missing
Alternate Hypothesis: The distribution of result is different depending on whether ban1 is missing

After performing a permutation test, the resulting p-value is 0.55. Since this value is greater than 0.5, we fail to reject the null hypothesis and determine that this result is not significant. This means that the missingness of bans likely does not depend on the result columns.

<iframe
  src="assets/missingness_bans.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing:
In this hypothesis test, I will determine if there is a significant difference for monster kills and winning games.

Null: There is no association between the number of monster kills and the number of wins.
Alternate: There is a positive association between the number of monster kills and the number of wins.
Test Statistic: difference in means
Significance Level: 5%

To do this I used permutation test since the distribution of the sample is not completely known.

<iframe
  src="assets/hypothesis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The resulting P-value is incredibly small (less than 0.000) because of the observed difference being so extreme. Therefore, we can reject the null hypothesis and say that more monster kills most likely do impact the chance of winning the game because the result is very significant.

## Framing a Prediction Problem
Now that I know a correlation between monster kills and the result of the game is likely, I want to see if I can predict the result of the game based on this information. The variable I will be predicting is 'result'. I will use binary classification because I just need to determine if the outcome is a win or a loss.

## Baseline Model
To do this I will employ machine learning techniques to train a model and see how well it can predict the outcome of games based on monster kills and gold accumulated. Gold accumulated is closely linked with monster kills because killing monsters rewards players with extra resources like gold. A standard scaler will be applied to the totalgold and monsterkills columns in order to transform them since they are both quantitative variables. The data will then be split into an 80/20 split with training and test in order to help mitigate overfitting.

The resulting baseline model is able to predict the outcome of the game with 70.5% accuracy with the given variables. It does seem to do a slightly better job of predicting wins than losses as seen by the 73% recall rate for wins and 68% recall rate for losses. However, it doesn't seem to show any significant bias. While this is a good start, it isn't able to predict the result with too much confidence. Some improvements to the model will be necessary.

## Final Model
In order to improve the accuracy of the previous model, I decided to incorporate some additional variables. I previously discovered that teams that had more monster kills also tended to have more kills, more assists, and less deaths. This is likely the case because as a team gets more monster kills, they amass more resources which allows them to perform better in other aspects of the game such as against other players. With this in mind, I decided to use a grid search in order to verify which variables would result in the best performance of the model. After determining the best variables to use (which ended up being the variables that were found with the aggregates), the final model could be run on the data.The resulting model has an accuracy of 96% which is a significant improvement over the baseline model. The recall rates for both winning and losing are now roughly the same. Ultimately, this means that the model is very good at predicting the result of a game based on the given data.

## Fairness Analysis
In order to test the fairness of my model, I decided to ask the question: does my model perform worse for short games (games that have a runtime less than 2000) that is does for long games (games that have a runtime greater than or equal to 2000)? To solve this I used a permutation test.

Null hypothesis: My model is fair and its accuracy for short games is the same as the accuracy for long games.
Alternative hypothesis: Our model is unfair and its accuracy for short games is not the same as the accuracy for long games.

The permutation test resulted in a p-value of 0.05 which is less than 0.05. This means that the value is significant and that the model is unfair. The model has a harder time predicting the outcome of longer games. In order to find out why, I decided to perform analysis on the short and long games. I made distributions for these games on whether they won or lost and distributed them over the total amount of gold, which is accumulated as a result of killing monsters among other things. 

<iframe
  src="assets/gold_short.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/gold_long.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This resulted in a clear difference in the distributions between long and short games. For games that go on longer, the distributions of total gold is closer than it is for short games. This makes sense because as the game goes on, the team that killed more monsters and accumulated their resources earlier on run out of ways to level up or upgrade their gear. This gives the team that did not have the advatange to start to close the gap between the two teams as they are given more time. This results in a definite winner being harder to predict based on resource gathering because of the fact that at a certain point, both teams will eventually be maximum level and have the best gear, meaning that the value of resources is decreased significantly and therefore matters less in the overall outcome of the game.

## Conclusion
In conclusion, it can be determined that, according to the data, a winning strategy is to kill monsters and focus on gathering resources in the early game. Then once enough of a resource advantage is garnered, all aspects of the game become easier to perform. Using this advantage, teams should press their advantage and try to close out the game as soon as possible before the enemy team has enough time to recoup and make up the resource disadvantage. Teams who don't focus on their resource management or don't press their advantage in the late game are statistically more likely to lose.
