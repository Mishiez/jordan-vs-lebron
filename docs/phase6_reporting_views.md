# Phase 6: Reporting Views

## Overview

This phase created 10 SQL views that serve as the data source for Power BI. Each view answers one or more of the 7 core questions, providing clean, aggregated data ready for visualization.

---

## Views Created

| # | View Name | Purpose | Questions Answered |
|---|-----------|---------|-------------------|
| 1 | `vw_ppg_comparison` | PPG by player and game type | Q1 |
| 2 | `vw_season_ppg` | Season-by-season scoring trends | Q1, Q6 |
| 3 | `vw_longevity` | Total games and minutes | Q2 |
| 4 | `vw_win_percentage` | Win % by opponent strength | Q3 |
| 5 | `vw_consistency` | Consistency metrics + triple-doubles | Q4, Q7 |
| 6 | `vw_playoff_lift` | Playoff vs regular season lift | Q5 |
| 7 | `vw_finals_performance` | Finals-specific statistics | Q5 |
| 8 | `vw_peak_performance` | Best games and best stretches | Q6 |
| 9 | `vw_all_around` | Combined stats and weighted scores | Q7 |
| 10 | `vw_age_analysis` | Performance by age | Q6, Q7 |

---

## View Details

### 1. `vw_ppg_comparison`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| game_type | Regular Season or Playoffs |
| ppg | Points per game average |
| games | Number of games |
| playoff_lift | Playoff PPG minus Regular PPG (NULL for playoff rows) |

**Sample Data:**
| player | game_type | ppg | games | playoff_lift |
|--------|-----------|-----|-------|--------------|
| Jordan | Regular Season | 30.5 | 1042 | 3.0 |
| Jordan | Playoffs | 33.5 | 177 | NULL |
| LeBron | Regular Season | 27.3 | 1211 | 1.6 |
| LeBron | Playoffs | 28.9 | 255 | NULL |

---

### 2. `vw_season_ppg`

| Column | Description |
|--------|-------------|
| season | Calendar year |
| jordan_ppg | Jordan's PPG that season (NULL if not played) |
| jordan_games | Jordan's games that season |
| lebron_ppg | LeBron's PPG that season (NULL if not played) |
| lebron_games | LeBron's games that season |

**Sample Data:**
| season | jordan_ppg | lebron_ppg |
|--------|-----------|------------|
| 1988 | 35.8 | NULL |
| 2006 | NULL | 30.4 |
| 2003 | 22.7 | 21.6 |

---

### 3. `vw_longevity`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| total_games | Career games played |
| total_minutes | Career minutes played |
| avg_minutes | Average minutes per game |
| min_minutes | Lowest minutes in a game |
| max_minutes | Highest minutes in a game |

**Sample Data:**
| player | total_games | total_minutes | avg_minutes |
|--------|-------------|---------------|-------------|
| Jordan | 1042 | 40,061 | 38.4 |
| LeBron | 1211 | 46,619 | 38.5 |

---

### 4. `vw_win_percentage`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| opponent_strength | Above .500 or Below .500 |
| games | Number of games |
| wins | Number of wins |
| win_pct | Win percentage |

**Sample Data:**
| player | opponent_strength | games | wins | win_pct |
|--------|-------------------|-------|------|---------|
| Jordan | Above .500 | 1018 | 678 | 66.6 |
| Jordan | Below .500 | 24 | 11 | 45.8 |

---

### 5. `vw_consistency`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| std_dev_ppg | Standard deviation of points per game |
| pct_bad_games | % of games with under 15 points |
| pct_great_games | % of games with 40+ points |
| pct_typical_games | % of games between 20-30 points |
| triple_doubles | Number of triple-doubles (10+ PTS, AST, TRB) |

**Sample Data:**
| player | std_dev_ppg | pct_bad_games | pct_great_games | triple_doubles |
|--------|-------------|---------------|-----------------|----------------|
| Jordan | 9.5 | 4.1 | 16.6 | 27 |
| LeBron | 7.8 | 3.8 | 5.4 | 94 |

---

### 6. `vw_playoff_lift`

| Column | Description |
|--------|-------------|
| season | Year of the season |
| player | Jordan or LeBron |
| regular_ppg | Regular season PPG |
| playoff_ppg | Playoff PPG |
| playoff_lift | Playoff PPG minus Regular PPG |

**Sample Data:**
| season | player | regular_ppg | playoff_ppg | playoff_lift |
|--------|--------|-------------|-------------|--------------|
| 1986 | Jordan | 32.1 | 43.7 | 11.5 |
| 2009 | LeBron | 29.2 | 35.3 | 6.1 |

---

### 7. `vw_finals_performance`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| finals_games | Number of Finals games played |
| avg_pts | Average points in Finals |
| avg_ast | Average assists in Finals |
| avg_trb | Average rebounds in Finals |
| wins | Number of Finals wins |
| win_pct | Finals win percentage |

**Sample Data:**
| player | finals_games | avg_pts | wins | win_pct |
|--------|--------------|---------|------|---------|
| Jordan | 34 | 33.9 | 24 | 70.6 |
| LeBron | 54 | 28.6 | 22 | 40.7 |

---

### 8. `vw_peak_performance`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| metric | Type of peak metric |
| value | The value (points or average) |
| game_date | Date of game (NULL for stretch averages) |
| opp | Opponent (NULL for stretch averages) |
| is_win | Whether game was won (NULL for stretch averages) |

**Sample Data:**
| player | metric | value | game_date | opp |
|--------|--------|-------|-----------|-----|
| Jordan | Highest Scoring Game | 69.0 | 1990-03-28 | CLE |
| Jordan | Best 10-Game Avg (PPG) | 38.6 | NULL | NULL |

---

### 9. `vw_all_around`

| Column | Description |
|--------|-------------|
| player | Jordan or LeBron |
| avg_pts | Average points per game |
| avg_ast | Average assists per game |
| avg_trb | Average rebounds per game |
| raw_combined | PTS + AST + TRB average |
| weighted_score | PTS + 1.5(AST) + 1.2(TRB) |
| triple_doubles | Total triple-doubles |
| triple_double_pct | % of games with triple-double |

**Sample Data:**
| player | raw_combined | weighted_score | triple_doubles |
|--------|--------------|----------------|----------------|
| Jordan | 42.0 | 45.9 | 27 |
| LeBron | 42.2 | 47.4 | 94 |

---

### 10. `vw_age_analysis`

| Column | Description |
|--------|-------------|
| age | Player age (years) |
| player | Jordan or LeBron |
| avg_ppg | Average points at that age |
| win_pct | Win percentage at that age |
| games | Number of games at that age |

**Sample Data:**
| age | player | avg_ppg | win_pct |
|-----|--------|---------|---------|
| 21 | Jordan | 28.1 | 49.0 |
| 21 | LeBron | 30.4 | 59.5 |
| 25 | Jordan | 35.8 | 60.3 |
| 25 | LeBron | 28.0 | 77.9 |

---

## Power BI Connection Instructions

### Step 1: Connect to MySQL
1. Open Power BI Desktop
2. Click **Get Data** → **Database** → **MySQL Database**
3. Enter server: `localhost:3306`
4. Enter database: `jordan_vs_lebron`

### Step 2: Select Views
Select these views to import:
- ☑ vw_ppg_comparison
- ☑ vw_season_ppg
- ☑ vw_longevity
- ☑ vw_win_percentage
- ☑ vw_consistency
- ☑ vw_playoff_lift
- ☑ vw_finals_performance
- ☑ vw_peak_performance
- ☑ vw_all_around
- ☑ vw_age_analysis

### Step 3: Load and Model
- Click **Load** to import all views
- No relationships needed between views (they are independent summary tables)

---

## Verification Checklist

| View | Status | Data Quality |
|------|--------|--------------|
| vw_ppg_comparison | ✅ | 4 rows, correct values |
| vw_season_ppg | ✅ | 34 rows, covers 1985-2020 |
| vw_longevity | ✅ | 2 rows, totals match EDA |
| vw_win_percentage | ✅ | 4 rows, 66.1% overall for both |
| vw_consistency | ✅ | 2 rows, triple-doubles correct |
| vw_playoff_lift | ✅ | 28 rows, covers all playoff seasons |
| vw_finals_performance | ✅ | 2 rows, 70.6% vs 40.7% |
| vw_peak_performance | ✅ | 4 rows, 69 vs 61 points |
| vw_all_around | ✅ | 2 rows, 94 vs 27 triple-doubles |
| vw_age_analysis | ✅ | 21 rows, ages 18-40 |

---

## Next Steps

Proceed to **Phase 7: Power BI Dashboard**