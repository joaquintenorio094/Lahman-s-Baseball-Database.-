# Lahman-s-Baseball-Database.-
A Python project to analyze Lahman's baseball database
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from datetime import datetime
from datetime import date

people = pd.read_csv("core/People.csv")
batting = pd.read_csv("core/Batting.csv")
collegeplaying = pd.read_csv("core\CollegePlaying.csv")
teams = pd.read_csv("upstream\Teams.csv")
pitching = pd.read_csv("core\PitchingPost.csv")

# Merge people and batting tables on playerID

p_people = people[["playerID", "weight", "height", "bats",
                   "throws", "debut", "finalGame", "retroID", "bbrefID", "nameFirst", "nameLast", "birthYear", "birthMonth", "birthDay"]]
p_b = p_people.merge(batting, on="playerID")
print(p_b.head(5))


# filteroutdates
start_date = "2019-01-01"
end_date = "2020-08-18"

after_start_date = p_b["finalGame"] >= start_date
before_end_date = p_b["finalGame"] <= end_date
between_two_dates = after_start_date & before_end_date
lp_bfina = p_b.loc[between_two_dates]

# filterplayers with less than 50 games
activeplayers = p_bfinal[p_bfinal["G"] > 49]

activeplayers["fullname"] = activeplayers["nameFirst"] .str.cat(
    activeplayers["nameLast"], sep=" ")

columns = ["nameFirst", "nameLast"]

activeplayers.drop(columns, axis=1, inplace=True)

# Which active player had the most runs batted in (“RBI” from the Batting table) from 2015-2018?
activeplayers.sort_values(by=['RBI'], inplace=True, ascending=False)
years = [2015, 2016, 2017, 2018]
RBIyears = activeplayers[activeplayers.yearID.isin(years)]

aggregation_functions = {'RBI': 'sum', 'fullname': 'first'}
RBInew = RBIyears.groupby(
    RBIyears['fullname']).aggregate(aggregation_functions)

RBInew.sort_values(by='RBI', inplace=True, ascending=False)

print(RBInew.head())


# How many double plays did Albert Pujols ground into (“GIDP” from Batting table) in 2016?
GIDPyear = activeplayers[activeplayers["yearID"] == 2016]
GIDPplayer = GIDPyear[GIDPyear["fullname"] == "Albert Pujols"]


print(GIDPplayer[["fullname", "GIDP"]])


# SCATTERPLOT scatter plot relating triples (3B) and steals (SB)
plt.scatter(batting['3B'], batting["SB"])
plt.show()


# HISTOGRAM A histogram of triples (3B) per year.
batting_triplets = batting.groupby("yearID")["3B"].sum()
batting_triplets.hist(bins=30)


# Which college produced more players?

moreplayers = collegeplaying["schoolID"].value_counts()
print(moreplayers.head())
moreplayers.iloc[0:7].plot()

# Which team has won the World Series with most attendance in the same year?
teams_1 = teams[['name', 'attendance', 'yearID', 'WSWin']]
wsteams = teams_1[teams_1.WSWin != "N"]

wsteams.sort_values(by='attendance', ascending=False)

# Which player won the most games with wild pitchs during post season?

pitching['playerID'] = pitching['playerID'].str[:-2]
pitching.drop(pitching.columns.difference(
    ['playerID', 'W', 'L', 'WP']), 1, inplace=True)
pitching.sort_values(by="WP", ascending=False)
aggregation_functions = {'W': 'sum',
                         'WP': 'sum', 'L': 'sum', 'playerID': 'first'}
df_new = pitching.groupby(
    pitching['playerID']).aggregate(aggregation_functions)
df_new.sort_values(by='WP', ascending=False)
