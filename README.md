# 🏀 NBA Power BI Analytics Dashboard

## 📌 Project Overview
This project presents an interactive **NBA Analytics Dashboard** built using **Power BI**, leveraging historical NBA data to analyze **team performance, player statistics, game outcomes, and league rankings**.

The dashboard is designed with a clean **basketball-themed UI** and follows proper **data modeling and DAX best practices**.

---

## 📊 Dataset Description
The dataset consists of multiple CSV files related to NBA games, players, teams, and standings:

- **teams.csv** – Team metadata (city, arena, founding year)
- **players.csv** – Player information and team association
- **games.csv** – Game-level details (date, season, home/away points)
- **games_details.csv** – Player-level performance per game (points, rebounds, assists, etc.)
- **ranking.csv** – Team standings, win/loss records, conference data

---

## 🧱 Data Modeling (Star Schema)

- **Fact Table:** `games_details`
- **Dimension Tables:** `players`, `teams`, `games`, `ranking`, `DateTable`

### Relationships:
- `players[PLAYER_ID] → games_details[PLAYER_ID]`
- `teams[TEAM_ID] → games_details[TEAM_ID]`
- `games[GAME_ID] → games_details[GAME_ID]`
- `teams[TEAM_ID] → ranking[TEAM_ID]`
- `DateTable[Date] → games[GAME_DATE_EST]`
- `DateTable[Date] → ranking[STANDINGSDATE]`

---

## 📄 Dashboard Pages

### 1️⃣ Overview
- KPI Cards: Total Points, Total Games
- Season slicer
- Conference filter

### 2️⃣ Team Analysis
- Wins vs Losses (Clustered Column Chart)
- Home vs Away Points (Stacked Column Chart)
- Top Teams by Total Points (Bar Chart)

### 3️⃣ Player Analysis
- Top 10 Scorers (Bar Chart)
- Player Statistics Table
- Player Performance Trend (Line Chart)

### 4️⃣ Rankings
- Conference Standings Table
- Win Percentage Trend over Time (Line Chart)

---

## 🧮 Key DAX Measures

```DAX
Total Points = SUM ( games_details[PTS] )
Total Rebounds = SUM ( games_details[REB] )
Total Assists = SUM ( games_details[AST] )

Games Played = DISTINCTCOUNT ( games_details[GAME_ID] )

Points Per Game =
DIVIDE ( [Total Points], [Games Played] )

Win Percentage =
AVERAGE ( ranking[WIN_PCT] )

Games Behind =
DIVIDE (
    ([Leader Wins] - [Team Wins]) +
    ([Team Losses] - [Leader Losses]),
    2
)
