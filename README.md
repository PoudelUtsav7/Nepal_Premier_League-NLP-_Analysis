## 🇳🇵 Nepal Premier League - Cricket Analytics Dashboard
An end-to-end data analytics project covering the Nepal Premier Leagure (NPL), combining data collection, cleaning, transformation, and interactive Power BI dashboards batting and bowling performance analysis

----

## Project Overview
The Nepal Premier League is Nepal's premier T20 cricket tournament featuring local and international players across 8 franchises. This project collects innings-level data from all 32 matches, cleans and transforms it into analysis-ready datasets, and visualizes performance insights through interactive Power BI dashboards.

----

## Objective
The primary goal of this project is to support player buying decisions by identifying:

The top 3 batsmen based on runs, strike rate, batting average, and boundary %
The top 3 bowlers based on wickets, economy rate, bowling average, and strike rate
All dashboards and metrics are designed to support this selection process using real NPL match data.

---

## Datasets
Data was collected from ESPNcricinfo covering all 32 NPL matches.

| Dataset | Description |
|---|---|
| `batting_combined_` | Runs, balls, 4s, 6s, strike rate, dismissal |
| `bowling_combined_` | Overs, wickets, runs, economy, wides, no-balls |
| `player_info_` | Batting style, bowling style, role, country, name |

----

## Data Cleaning and Transformation
All cleaning done in main.ipynb using pandas:
- Merged data from two collection runs (matches 1-20 and 21 -32) using `pd.concat` with `drop_duplicates()`
- Stripped captain (c) and other suffixes from player names
- Cleaned team names using `.str.split('(').str[0].str.strip()`
- Validated data types and shapes across all datasets
- and so forth and so on... 

---

# Power BI Dashboard
Dashboard 1 : 
<img width="1276" height="714" alt="image" src="https://github.com/user-attachments/assets/5bde97d7-6817-41bd-ad92-ab6f50619a12" />

Dashboard 2: 
<img width="1286" height="721" alt="image" src="https://github.com/user-attachments/assets/f204661c-1e2c-414d-9bc7-87c6422bf13e" />

---

## Key DAX Measures
Batting: 
- Total Runs = SUM(batting_combined[runs])
- Total Innings Batted = DISTINCTCOUNT(batting_combined[match_id])
- Strike Rate = DIVIDE([Total Runs], [Total Ball Faced], 0)*100
- Highest Score = MAX(batting_combined[runs])
- Boundary % = DIVIDE(SUM(batting_combined[Boundary Runs]), [Total Runs], 0) * 100
- Batting Average = DIVIDE([Total Runs], [Total Innings Batted], 0)

Bowling:
- Wickets = SUM(bowling_combined[wickets])
- Total Innings Bowled = DISTINCTCOUNT(bowling_combined[match_id])
- Run Conceded = SUM(bowling_combined[runs])
- Economy = DIVIDE([Run Conceded], ([balls bowled]/ 6), 0)
- Bowling Strike Rate = DIVIDE([balls bowled], [Wickets])
- Bowling Average = DIVIDE([Run Conceded], [Wickets])
- balls bowled = SUM(bowling_combined[Balls])

**Batting Metrics**
- Total Runs :
  Total number of runs scored by the batsman.

- Total Innings Batted :
  Total number of matches/innings played by the batsman.

- Strike Rate :
  Measures how quickly a batsman scores runs.  
  Calculated as runs scored per 100 balls faced.

- Highest Score :
  Highest runs scored by the batsman in a single match.

- Boundary % :
  Percentage of total runs scored through boundaries (4s and 6s).

- Batting Average :
  Average runs scored per innings.

---

**Bowling Metrics**

- Wickets
  Total wickets taken by the bowler.

- Total Innings Bowled
  Total matches/innings bowled by the player.

- Run Conceded
  Total runs given by the bowler.

- Economy Rate
  Average runs conceded per over.

- Bowling Strike Rate
  Average number of balls needed to take one wicket.

- Bowling Average
  Average runs conceded per wicket taken.

- Balls Bowled
  Total balls delivered by the bowler.

---

## Metric Interpretation

| Metric | Better Value |
|---|---|
| Batting Average | Higher |
| Strike Rate | Higher |
| Boundary % | Higher |
| Economy Rate | Lower |
| Bowling Strike Rate | Lower |
| Bowling Average | Lower |


## Teams Covered
Janakpur Bolts  Kathmandu Gorkhas  Chitwan Rhinos  Karnali Yaks  Biratnagar Kings  Pokhara Avengers Lumbini Lions  Sudur Paschim Royals

