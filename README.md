# League of Legends Monster Kills vs Win Rates
DSC80 Project at UCSD about data analysis on tournament data from League of Legends.

The purpose of this project is to conduct analysis on League of Legends tournament data in order to extract valuable data regarding optimal strategies that can be taken to increase the odds of winning more games.

Author: Yadushan Thillainathan

## Introduction:
League of Legends is a popular game in the MOBA genre that amassed an extremely large player base and has made strides in the world of esports as it is one of the forefronts of tournament play for video games in the modern age. The dataset that is covered in this project is comprised of tournament data from the League of Legends world championship in 2022. The dataset in questions covers a wide variety of data including information regarding the team (eg character picks, character bans, etc.), player performance data (eg kills, deaths, assists, etc.), and match data (monsters killed, gold accumulated, etc.). 

For the purposes of this project, I decided to focus my efforts into the match data. In the game, players must balance their gameplay between fighting for the main objective, slaying enemy players, and accumulating resources. A large part of this is defeating monsters and minions in order to accumulate gold and experience point so that fighting against players and enemy towers becomes a much easier task. 

The central question this project is focused around is: do teams who kill more monsters win more games? This question will be answered by conducting data analysis on the dataset to see if any trends appear between wins and monster kills and then using this information to make a predictive model that might be able to determine if a team will win based on this data.

### Columns:
The dataset contains a very extensive array of data to analyze, but for the purpose of this project, the one that we will focus on are as follows.

'monsterkills': This column consists of the amount of monsters that were killed by each player and team
'totalgold': This columns includes the amount of gold that each player and team accumulated throughout the match
'kills': This columns includes the amount of kills on enemy players that each player and team accumulated throughout the match
'minionkills': This columns includes the amount of kills on enemy minions that each player and team accumulated throughout the match
'deaths': This columns includes the amount of deaths that each player and team accumulated throughout the match
'assists': This columns includes the amount of assists on enemy minions that each player and team accumulated throughout the match
'goldspent': This columns includes the amount of gold that each player and team spent throughout the match

## Data Cleaning and Exploratory Data Analysis:
### Data Cleaning:
The first step of the data cleaning process is to drop all of the data regarding individual players. For the purposes of this project is to analyze team performance, not individual. This data set has rows for players followed by rows of data from teams, so we will only keep this team data. Then, not all rows are complete and this is shown by the datacompleteness column which tells if the row is complete or not. All rows that are not complete are droppped. 

### Univariate Analysis:
The graph below shows the distribution of monster kills for teams that won.

The graph below shows the distribution of monster kills for teams that lost.

When overlaying these graphs over one another we can see that teams that won did tend to have more monster kills on average than teams that lost.

### Bivariate Analysis:
I graphed the percentage of teams that had more monster kills than the other by whether they won or lost. This graph shows that teams that had more monster kills definitely won more often than they lost. This seems to support the fact that monster kills have a positive relationship with win rates. 

### Interesting Aggregates:
When grouping by the result, we can find some very interesting aggregates. This shows that teams that won had more monster kills, more minion kills, more kills, more assists, more gold accumulated, and less deaths.

## Assessment of Missingness:

## Hypothesis Testing:
In this hypothesis test, I will determine if there is a significant difference for monster kills and winning games.

Null: There is no association between the number of monster kills and the number of wins.
Alternate: There is a positive association between the number of monster kills and the number of wins.
Test Statistic:
Significance Level: 5%

To do this I used Logisitic Regression since this is a binary classification task. 

According to the model, the resulting coefficient and intercept are: Coefficient: 0.009717630776798814 and Intercept: -1.8503285496480981

This means the model predicts that for every additional monster kill, the likelihood of winning increases be roughyly 0.0097. 

Using this we can find a p-value. The resulting P-value is incredibly small so we can reject the null hypothesis and say that more monster kills most likely do impact the chance of winning the game.

## Framing a Prediction Problem
Now that I know a correlation between monster kills and the result of the game is likely, I want to see if I can predict the result of the game based on this information. To do this I will employ machine learning techniques to train a model and see how well it can predict the outcome of games based on monster kills and gold accumulated. Gold accumulated is closely linked with monster kills because killing monsters rewards players with extra resources like gold. A standard scaler will be applied to the totalgold and monsterkills columns in order to transform them. The data will then be split into an 80/20 split with training and test in order to help mitigate overfitting.

## Baseline Model
The resulting baseline model is able to predict the outcome of the game with 70.5% accuracy with the given variables. It does seem to do a slightly better job of predicting wins than losses as seen by the 73% recall rate for wins and 68% recall rate for losses. However, it doesn't seem to show any significant bias.

## Final Model
In order to improve the accuracy of the previous model, I decided to incorporate some additional variables. I previously discovered that teams that had more monster kills also tended to have more kills, more assists, and less deaths, so I have decided to add those to my model to see if that could lead to improved accuracy in the model.

The resulting model has an accuracy of 96% which is a significant improvement over the baseline model. The recall rates for both winning and losing are now roughly the same. Ultimately, this means that the model is very good at predicting the result of a game based on the given data.

## Fairness Analysis

## Conclusion
