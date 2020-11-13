# Lahman-s-Baseball-Database<br />
A Python project to analyze Lahman's baseball database<br />




Connects to an SQL database file and queries for all players who have played at least 50 games and are still active.  Use the “finalGame” field from the “People” table to determine if a player is active. Retrieve weight, throws, bats, throws, all birth-related and all name-related columns from the “People” table and retrieve all columns from the “Batting” table.<br />
Converts this data into either an R data frame or a pandas data frame.<br />
Adds a calculated column with the player’s age and a calculated column with each player’s first and last name concatenated.<br />
Once the calculated columns are added, drops the other columns related to birth date and name.<br />
Deletes any rows with missing values<br />
Answers the following questions<br />
 
Which active player had the most runs batted in (“RBI” from the Batting table) from 2015-2018?<br />
How many double plays did Albert Pujols ground into (“GIDP” from Batting table) in 2016?<br />
 
Creates the following plots:<br />
 
A histogram of triples (3B) per year.<br />
Create a scatter plot relating triples (3B) and steals (SB).<br />
 
Comes up at least three additional questions about the data and answers them. At least one should be a question about the relationship between two variables, e.g., triples and steals, as above.<br />
 
To meet these requirements you will need to research additional packages and/or functionality from existing packages:<br />
<br />
 

Connecting to an SQL database file and performing SQL queries. For Python, use the popular package sqlite3 and for R use RSQLite.<br />
Manipulating data, in this case for adding and removing columns, rearranging and grouping, etc. In Python, the pandas package should provide the necessary functionality; read the documentation to find out more. For R, the dplyr package is the most popular choice.
