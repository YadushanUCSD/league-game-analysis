# League of Legends Monster Kills vs Win Rates
DSC80 Project at UCSD about data analysis on tournament data from League of Legends.

The purpose of this project is to conduct analysis on League of Legends tournament data in order to extract valuable data regarding optimal strategies that can be taken to increase the odds of winning more games.

Author: Yadushan Thillainathan

## Introduction:
League of Legends is a popular game in the MOBA genre that amassed an extremely large player base and has made strides in the world of esports as it is one of the forefronts of tournament play for video games in the modern age. The dataset that is covered in this project is comprised of tournament data from the League of Legends world championship in 2022. The dataset in questions covers a wide variety of data including information regarding the team (eg character picks, character bans, etc.), player performance data (eg kills, deaths, assists, etc.), and match data (monsters killed, gold accumulated, etc.). 

In the world of comeptitive gaming, any advantage gained over the other team is a means for victory. This includes strategy. The team with the best strategy will naturally win the most games. For the purposes of this project, I decided to focus my efforts into the match data. In the game, players must balance their gameplay between fighting for the main objective, slaying enemy players, and accumulating resources. A large part of this is defeating monsters and minions in order to accumulate gold and experience point so that fighting against players and enemy towers becomes a much easier task. 

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

<pre>|    | gameid                | datacompleteness   |   url | league   |   year | split   |   playoffs | date                |   game |   patch |   participantid | side   | position   |   playername |   playerid | teamname                 | teamid                                  |   champion | ban1    | ban2         | ban3         | ban4     | ban5    | pick1    | pick2   | pick3    | pick4    | pick5     |   gamelength |   result |   kills |   deaths |   assists |   teamkills |   teamdeaths |   doublekills |   triplekills |   quadrakills |   pentakills |   firstblood |   firstbloodkill |   firstbloodassist |   firstbloodvictim |   team kpm |   ckpm |   firstdragon |   dragons |   opp_dragons |   elementaldrakes |   opp_elementaldrakes |   infernals |   mountains |   clouds |   oceans |   chemtechs |   hextechs |   dragons (type unknown) |   elders |   opp_elders |   firstherald |   heralds |   opp_heralds |   void_grubs |   opp_void_grubs |   firstbaron |   barons |   opp_barons |   firsttower |   towers |   opp_towers |   firstmidtower |   firsttothreetowers |   turretplates |   opp_turretplates |   inhibitors |   opp_inhibitors |   damagetochampions |     dpm |   damageshare |   damagetakenperminute |   damagemitigatedperminute |   wardsplaced |    wpm |   wardskilled |   wcpm |   controlwardsbought |   visionscore |   vspm |   totalgold |   earnedgold |   earned gpm |   earnedgoldshare |   goldspent |       gspd |   gpr |   total cs |   minionkills |   monsterkills |   monsterkillsownjungle |   monsterkillsenemyjungle |    cspm |   goldat10 |   xpat10 |   csat10 |   opp_goldat10 |   opp_xpat10 |   opp_csat10 |   golddiffat10 |   xpdiffat10 |   csdiffat10 |   killsat10 |   assistsat10 |   deathsat10 |   opp_killsat10 |   opp_assistsat10 |   opp_deathsat10 |   goldat15 |   xpat15 |   csat15 |   opp_goldat15 |   opp_xpat15 |   opp_csat15 |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsat15 |   assistsat15 |   deathsat15 |   opp_killsat15 |   opp_assistsat15 |   opp_deathsat15 |   goldat20 |   xpat20 |   csat20 |   opp_goldat20 |   opp_xpat20 |   opp_csat20 |   golddiffat20 |   xpdiffat20 |   csdiffat20 |   killsat20 |   assistsat20 |   deathsat20 |   opp_killsat20 |   opp_assistsat20 |   opp_deathsat20 |   goldat25 |   xpat25 |   csat25 |   opp_goldat25 |   opp_xpat25 |   opp_csat25 |   golddiffat25 |   xpdiffat25 |   csdiffat25 |   killsat25 |   assistsat25 |   deathsat25 |   opp_killsat25 |   opp_assistsat25 |   opp_deathsat25 | bans_missing   |   Intercept |\n|---:|:----------------------|:-------------------|------:|:---------|-------:|:--------|-----------:|:--------------------|-------:|--------:|----------------:|:-------|:-----------|-------------:|-----------:|:-------------------------|:----------------------------------------|-----------:|:--------|:-------------|:-------------|:---------|:--------|:---------|:--------|:---------|:---------|:----------|-------------:|---------:|--------:|---------:|----------:|------------:|-------------:|--------------:|--------------:|--------------:|-------------:|-------------:|-----------------:|-------------------:|-------------------:|-----------:|-------:|--------------:|----------:|--------------:|------------------:|----------------------:|------------:|------------:|---------:|---------:|------------:|-----------:|-------------------------:|---------:|-------------:|--------------:|----------:|--------------:|-------------:|-----------------:|-------------:|---------:|-------------:|-------------:|---------:|-------------:|----------------:|---------------------:|---------------:|-------------------:|-------------:|-----------------:|--------------------:|--------:|--------------:|-----------------------:|---------------------------:|--------------:|-------:|--------------:|-------:|---------------------:|--------------:|-------:|------------:|-------------:|-------------:|------------------:|------------:|-----------:|------:|-----------:|--------------:|---------------:|------------------------:|--------------------------:|--------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|----------------:|------------------:|-----------------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|----------------:|------------------:|-----------------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|----------------:|------------------:|-----------------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|----------------:|------------------:|-----------------:|:---------------|------------:|\n| 10 | ESPORTSTMNT01_2690210 | complete           |   nan | LCKC     |   2022 | Spring  |          0 | 2022-01-10 07:44:08 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | BRION Challengers        | oe:team:733ebb9dbf22a401c0127a0c80193ca |        nan | Karma   | Caitlyn      | Syndra       | Thresh   | Lulu    | Renekton | Samira  | Xin Zhao | LeBlanc  | Leona     |         1713 |        0 |       9 |       19 |        19 |           9 |           19 |             0 |             0 |             0 |            0 |            1 |              nan |                nan |                nan |     0.3152 | 0.9807 |             0 |         1 |             3 |                 1 |                     3 |           0 |           0 |        0 |        0 |           0 |          1 |                      nan |        0 |            0 |             1 |         2 |             0 |          nan |              nan |            0 |        0 |            0 |            1 |        3 |            6 |               1 |                    1 |              5 |                  0 |            0 |                1 |               56560 | 1981.09 |           nan |                3537.2  |                    2364.73 |            74 | 2.5919 |            51 | 1.7863 |                   33 |           197 | 6.9002 |       47070 |        28222 |      988.511 |               nan |       44570 | -0.0283123 |  0.94 |        nan |           680 |            160 |                     nan |                       nan | 29.4221 |      16218 |    18213 |      322 |          14695 |        18076 |          330 |           1523 |          137 |           -8 |           3 |             5 |            0 |               0 |                 0 |                3 |      24806 |    28001 |      487 |          24699 |        29618 |          510 |            107 |        -1617 |          -23 |           5 |            10 |            6 |               6 |                18 |                5 |      31962 |    36874 |      631 |          32906 |        41821 |          715 |           -944 |        -4947 |          -84 |           5 |            10 |            7 |               7 |                22 |                5 |      40224 |    45960 |      767 |          40136 |        49931 |          864 |             88 |        -3971 |          -97 |           6 |            12 |            7 |               7 |                22 |                6 | False          |           1 |\n| 11 | ESPORTSTMNT01_2690210 | complete           |   nan | LCKC     |   2022 | Spring  |          0 | 2022-01-10 07:44:08 |      1 |   12.01 |             200 | Red    | team       |          nan |        nan | Nongshim Esports Academy | oe:team:7c64febcd5ccff13dcd035dc6867a00 |        nan | Lee Sin | Twisted Fate | Zoe          | Nautilus | Rell    | Jinx     | Viego   | Gragas   | Viktor   | Alistar   |         1713 |        1 |      19 |        9 |        62 |          19 |            9 |             6 |             0 |             0 |            0 |            0 |              nan |                nan |                nan |     0.6655 | 0.9807 |             1 |         3 |             1 |                 3 |                     1 |           2 |           1 |        0 |        0 |           0 |          0 |                      nan |        0 |            0 |             0 |         0 |             2 |          nan |              nan |            0 |        0 |            0 |            0 |        6 |            3 |               0 |                    0 |              0 |                  5 |            1 |                0 |               79912 | 2799.02 |           nan |                3009.67 |                    2872.33 |            93 | 3.2574 |            51 | 1.7863 |                   45 |           205 | 7.1804 |       52617 |        33769 |     1182.8   |               nan |       45850 |  0.0283123 | -0.94 |        nan |           792 |            184 |                     nan |                       nan | 34.1856 |      14695 |    18076 |      330 |          16218 |        18213 |          322 |          -1523 |         -137 |            8 |           0 |             0 |            3 |               3 |                 5 |                0 |      24699 |    29618 |      510 |          24806 |        28001 |          487 |           -107 |         1617 |           23 |           6 |            18 |            5 |               5 |                10 |                6 |      32906 |    41821 |      715 |          31962 |        36874 |          631 |            944 |         4947 |           84 |           7 |            22 |            5 |               5 |                10 |                7 |      40136 |    49931 |      864 |          40224 |        45960 |          767 |            -88 |         3971 |           97 |           7 |            22 |            6 |               6 |                12 |                7 | False          |           1 |\n| 22 | ESPORTSTMNT01_2690219 | complete           |   nan | LCKC     |   2022 | Spring  |          0 | 2022-01-10 08:38:24 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | T1 Esports Academy       | oe:team:731b7a9fd004cdbe2bcb3da795bce47 |        nan | Sona    | Jarvan IV    | Caitlyn      | Lulu     | Lucian  | Lee Sin  | Jhin    | Gragas   | Rakan    | Orianna   |         2114 |        0 |       3 |       16 |         7 |           3 |           16 |             0 |             0 |             0 |            0 |            0 |              nan |                nan |                nan |     0.0851 | 0.5393 |             0 |         1 |             4 |                 1 |                     4 |           0 |           1 |        0 |        0 |           0 |          0 |                      nan |        0 |            0 |             1 |         1 |             1 |          nan |              nan |            0 |        0 |            2 |            0 |        3 |           11 |               0 |                    0 |              2 |                  3 |            0 |                2 |               59579 | 1690.98 |           nan |                2984.02 |                    3109.61 |           119 | 3.3775 |            55 | 1.561  |                   47 |           277 | 7.8619 |       57629 |        34688 |      984.522 |               nan |       53945 | -0.207137  | -3.23 |        nan |           994 |            215 |                     nan |                       nan | 34.3141 |      14939 |    17462 |      317 |          16558 |        19048 |          344 |          -1619 |        -1586 |          -27 |           1 |             1 |            3 |               3 |                 3 |                1 |      23522 |    28848 |      533 |          25285 |        29754 |          555 |          -1763 |         -906 |          -22 |           1 |             1 |            3 |               3 |                 3 |                1 |      31228 |    38596 |      710 |          36368 |        42069 |          758 |          -5140 |        -3473 |          -48 |           1 |             1 |            5 |               5 |                 6 |                1 |      39335 |    49409 |      895 |          46615 |        57155 |          928 |          -7280 |        -7746 |          -33 |           1 |             1 |            8 |               8 |                13 |                1 | False          |           1 |\n| 23 | ESPORTSTMNT01_2690219 | complete           |   nan | LCKC     |   2022 | Spring  |          0 | 2022-01-10 08:38:24 |      1 |   12.01 |             200 | Red    | team       |          nan |        nan | Liiv SANDBOX Youth       | oe:team:e7a7c6bf58eb268ed3f13aac4158aa8 |        nan | LeBlanc | Yuumi        | Twisted Fate | Karma    | Alistar | Renekton | Syndra  | Nidalee  | Leona    | Gangplank |         2114 |        1 |      16 |        3 |        39 |          16 |            3 |             1 |             0 |             0 |            0 |            1 |              nan |                nan |                nan |     0.4541 | 0.5393 |             1 |         4 |             1 |                 4 |                     1 |           0 |           2 |        1 |        0 |           0 |          1 |                      nan |        0 |            0 |             0 |         1 |             1 |          nan |              nan |            1 |        2 |            0 |            1 |       11 |            3 |               1 |                    1 |              3 |                  2 |            2 |                0 |               74855 | 2124.55 |           nan |                2745.72 |                    2868.42 |           129 | 3.6613 |            70 | 1.9868 |                   65 |           346 | 9.8202 |       71004 |        48063 |     1364.13  |               nan |       66410 |  0.207137  |  3.23 |        nan |          1013 |            244 |                     nan |                       nan | 35.6764 |      16558 |    19048 |      344 |          14939 |        17462 |          317 |           1619 |         1586 |           27 |           3 |             3 |            1 |               1 |                 1 |                3 |      25285 |    29754 |      555 |          23522 |        28848 |          533 |           1763 |          906 |           22 |           3 |             3 |            1 |               1 |                 1 |                3 |      36368 |    42069 |      758 |          31228 |        38596 |          710 |           5140 |         3473 |           48 |           5 |             6 |            1 |               1 |                 1 |                5 |      46615 |    57155 |      928 |          39335 |        49409 |          895 |           7280 |         7746 |           33 |           8 |            13 |            1 |               1 |                 1 |                8 | False          |           1 |\n| 46 | ESPORTSTMNT01_2690227 | complete           |   nan | LCKC     |   2022 | Spring  |          0 | 2022-01-10 09:51:16 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | KT Rolster Challengers   | oe:team:b9733b8e8aa341319bbaf1035198a28 |        nan | Syndra  | Caitlyn      | Karma        | Gragas   | Vex     | Renekton | Talon   | Yuumi    | Aphelios | Zoe       |         1972 |        1 |      14 |        5 |        42 |          14 |            5 |             3 |             1 |             0 |            0 |            0 |              nan |                nan |                nan |     0.426  | 0.5781 |             1 |         4 |             1 |                 4 |                     1 |           0 |           1 |        0 |        1 |           0 |          2 |                      nan |        0 |            0 |             0 |         1 |             1 |          nan |              nan |            1 |        1 |            0 |            1 |       11 |            2 |               1 |                    1 |              1 |                  4 |            2 |                0 |               67376 | 2049.98 |           nan |                2327.89 |                    1776.27 |           119 | 3.6207 |            51 | 1.5517 |                   68 |           264 | 8.0325 |       62868 |        41372 |     1258.78  |               nan |       57615 |  0.165672  |  1.45 |        nan |           874 |            269 |                     nan |                       nan | 34.7769 |      15466 |    19600 |      368 |          15569 |        18787 |          355 |           -103 |          813 |           13 |           0 |             0 |            1 |               1 |                 1 |                0 |      24795 |    31342 |      560 |          23604 |        29044 |          545 |           1191 |         2298 |           15 |           3 |             8 |            1 |               1 |                 1 |                3 |      33717 |    41577 |      752 |          31973 |        39291 |          738 |           1744 |         2286 |           14 |           3 |             8 |            1 |               1 |                 1 |                3 |      43989 |    52441 |      912 |          39844 |        49909 |          907 |           4145 |         2532 |            5 |           5 |            12 |            2 |               2 |                 1 |                5 | False          |           1 |</pre>

### Univariate Analysis:
The graph below shows the distribution of monster kills for teams that won.

<iframe
  src="assets/univariate_win_only.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The graph below shows the distribution of monster kills for teams that lost.

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

### Bivariate Analysis:
I graphed the percentage of teams that had more monster kills than the other by whether they won or lost. This graph shows that teams that had more monster kills definitely won more often than they lost. This seems to support the fact that monster kills have a positive relationship with win rates. 

<iframe
  src="assets/bivariate_monster.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates:
When grouping by the result, we can find some very interesting aggregates. This shows that teams that won had more monster kills, more minion kills, more kills, more assists, more gold accumulated, and less deaths.

## Assessment of Missingness:
### NMAR Analysis
When looking at the data it appears that soeme of the incomplete data have missing values for some of the kill streaks, such as double kills, triple kills, etc. I don't believe that these are NMAR (not missing at random) because at the highest level of play, it might be hard to defeat multiple top players in a row, which is why kill streaks become a difficult task. As such, these values may be missing because its likely that they may never happen in a game at the competitive level. Since, the missingness of the data depends on itself, it makes sense that this would be NMAR. In order to make it MAR (missing at random), some additional data may be needed. For example, a column that states if any killstreaks occured during the game may result in the missingness of this killstreak data dependent on whether or not the anykillstreaks column is true or false.

### Missingness Dependency
When looking at the 

<iframe
  src="assets/missingness_firstblood.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

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
Test Statistic:
Significance Level: 5%

To do this I used Logisitic Regression since this is a binary classification task. 

According to the model, the resulting coefficient and intercept are: Coefficient: 0.009717630776798814 and Intercept: -1.8503285496480981

This means the model predicts that for every additional monster kill, the likelihood of winning increases be roughyly 0.0097. 

Using this we can find a p-value. The resulting P-value is incredibly small (less than 0.000) so we can reject the null hypothesis and say that more monster kills most likely do impact the chance of winning the game.

## Framing a Prediction Problem
Now that I know a correlation between monster kills and the result of the game is likely, I want to see if I can predict the result of the game based on this information. The variable I will be predicting is 'result'. I will use binary classification because I just need to determine if the outcome is a win or a loss.

## Baseline Model
To do this I will employ machine learning techniques to train a model and see how well it can predict the outcome of games based on monster kills and gold accumulated. Gold accumulated is closely linked with monster kills because killing monsters rewards players with extra resources like gold. A standard scaler will be applied to the totalgold and monsterkills columns in order to transform them. The data will then be split into an 80/20 split with training and test in order to help mitigate overfitting.

The resulting baseline model is able to predict the outcome of the game with 70.5% accuracy with the given variables. It does seem to do a slightly better job of predicting wins than losses as seen by the 73% recall rate for wins and 68% recall rate for losses. However, it doesn't seem to show any significant bias.

## Final Model
In order to improve the accuracy of the previous model, I decided to incorporate some additional variables. I previously discovered that teams that had more monster kills also tended to have more kills, more assists, and less deaths. This is likely the case because as a team gets more monster kills, they amass more resources which allows them to perform better in other aspects of the game such as against other players. Keeping this in mind, I have decided to add those to my model to see if that could lead to improved accuracy in the model.

The resulting model has an accuracy of 96% which is a significant improvement over the baseline model. The recall rates for both winning and losing are now roughly the same. Ultimately, this means that the model is very good at predicting the result of a game based on the given data.

## Fairness Analysis
In order to test the fairness of my model, I decided to ask the question: does my model perform worse for short games (games that have a runtime less than 2000) that is does for long games (games that have a runtime greater than or equal to 2000)? To solve this I used a permutation test.

Null hypothesis: My model is fair and its accuracy for short games is the same as the accuracy for long games.
Alternative hypothesis: Our model is unfair and its accuracy for short games is not the same as the accuracy for long games.

The permutation test resulted in a p-value of 0.05 which is less than 0.05. This means that the value is significant and that the model is unfair. The model has a harder time predicting the outcome of longer games. In order to find out why, I decided to perform analysis on the short and long games. I made distributions for these games on whether they won or lost and distributed them over the total amount of gold, which is accumulated as a result of killing monsters among other things. This resulted in a clear difference in the distributions between long and short games. For games that go on longer, the distributions of total gold is closer than it is for short games. This makes sense because as the game goes on, the team that killed more monsters and accumulated their resources earlier on run out of ways to level up or upgrade their gear. This gives the team that did not have the advatange to start to close the gap between the two teams as they are given more time. This results in a definite winner being harder to predict based on resource gathering because of the fact that at a certain point, both teams will eventually be maximum level and have the best gear, meaning that the value of resources is decreased significantly and therefore matters less in the overall outcome of the game.

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

## Conclusion
