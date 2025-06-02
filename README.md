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
