# Phase 1: Data Understanding

## Dataset Overview

This project analyzes game-level statistics for Michael Jordan and LeBron James across their entire careers.

### Data Volume

| Player | Regular Season Games | Playoff Games | Total |
|--------|---------------------|---------------|-------|
| Michael Jordan | 1,042 | 177 | 1,219 |
| LeBron James | 1,211 | 255 | 1,466 |
| **Combined** | 2,253 | 432 | 2,685 |

### Table Structure

| Table Name | Rows | Columns | Description |
|------------|------|---------|-------------|
| jordan_career | 1,042 | 26 | Jordan regular season games |
| jordan_playoffs | 177 | 27 | Jordan playoff games |
| lebron_career | 1,211 | 26 | LeBron regular season games |
| lebron_playoffs | 255 | 27 | LeBron playoff games |

## Column Reference

### Common Columns (All Tables)

| Column | Type | Meaning |
|--------|------|---------|
| game | INT | Game number within season (resets to 1 each season) |
| date | TEXT | Game date (YYYY-MM-DD) |
| team | TEXT | Player's team abbreviation |
| opp | TEXT | Opponent team abbreviation |
| result | TEXT | Win/Loss with point differential |
| mp | INT | Minutes played |
| fg, fga, fgp | INT, INT, DOUBLE | Field goals made, attempted, percentage |
| three, threeatt, threep | INT, INT, DOUBLE/TEXT | 3-pointers made, attempted, percentage |
| ft, fta, ftp | INT, INT, DOUBLE | Free throws made, attempted, percentage |
| orb, drb, trb | INT, INT, INT | Offensive, defensive, total rebounds |
| ast, stl, blk, tov | INT | Assists, steals, blocks, turnovers |
| pts | INT | Points scored |
| game_score | DOUBLE | Advanced productivity metric |
| plus_minus | INT/TEXT | Point differential while on court |

### Career-Only Columns

| Column | Type | Meaning |
|--------|------|---------|
| age | TEXT | Player age in "years-days" format (e.g., "21-252") |

### Playoff-Only Columns

| Column | Type | Meaning |
|--------|------|---------|
| series | TEXT | Playoff round (EC1, ECS, ECF, FIN, etc.) |
| series_game | INT | Game number within series (1, 2, 3...) |

## Table Relationships

- **Career ↔ Playoffs:** Connect by `date` (extract year to group by season)
- **Jordan ↔ LeBron:** No direct relationship - compare through aggregated analysis
- **No season column exists:** Must extract from `date` using `YEAR(date)`

## Data Quality Findings

### Issues Identified

| Table | Column | Current Type | Issue | Fix |
|-------|--------|--------------|-------|-----|
| jordan_career | threep | TEXT | Contains numeric strings | CAST to DOUBLE |
| jordan_career | plus_minus | TEXT | Empty strings, no data | Cannot use |
| jordan_career | age | TEXT | "21-252" format | Parse to decimal |
| jordan_playoffs | threep | TEXT | Contains numeric strings/empty | CAST to DOUBLE |
| jordan_playoffs | plus_minus | TEXT | Empty strings, no data | Cannot use |
| lebron_career | age | TEXT | "18-303" format | Parse to decimal |
| lebron_playoffs | (all) | Clean | No issues | None needed |

### Key Discovery: Plus/Minus Unavailable for Jordan

Jordan's data contains no plus/minus information (empty strings in all rows). This metric can only be analyzed for LeBron.

## Phase 1 Summary

✅ Data dictionaries reviewed  
✅ Column meanings documented  
✅ Table relationships identified  
✅ Data types cataloged  
✅ Inconsistencies found  
✅ Data quality issues logged  
✅ Limitations documented  

