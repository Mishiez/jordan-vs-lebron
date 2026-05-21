# 🏀 The GOAT Debate: Jordan vs LeBron - A Data-Driven Analysis

## Project Overview

This project analyzes **2,685 career games** to answer one of sports' most debated questions: **Who is the greatest basketball player of all time?**

Using **SQL** for data processing and **Power BI** for visualization, this analysis compares Michael Jordan and LeBron James across 7 measurable categories that anyone can understand—no basketball knowledge required.

---

## Phase 1: Dataset Understanding

### Data Sources

The dataset contains **game-level statistics** for both players' entire careers:

| Table Name | Description | Rows | Columns |
|------------|-------------|------|---------|
| `jordan_career` | Jordan regular season games | 1,042 | 26 |
| `jordan_playoffs` | Jordan playoff games | 177 | 27 |
| `lebron_career` | LeBron regular season games | 1,211 | 26 |
| `lebron_playoffs` | LeBron playoff games | 255 | 27 |

**Total:** 2,685 NBA games analyzed

### Key Columns

| Column | Meaning | Data Type |
|--------|---------|-----------|
| `pts` | Points scored in game | INT |
| `ast` | Assists | INT |
| `trb` | Total rebounds | INT |
| `mp` | Minutes played | INT |
| `game_score` | Single-game performance metric | DOUBLE |
| `plus_minus` | Point differential while on court | INT (LeBron), TEXT (Jordan - empty) |
| `threep` | 3-point percentage | DOUBLE (LeBron), TEXT (Jordan) |
| `age` | Player age at game | TEXT ("21-252" format, both players) |
| `series` | Playoff round | TEXT (playoffs only) |
| `series_game` | Game number in series | INT (playoffs only) |

### Data Quality Findings

| Issue | Jordan | LeBron | Action |
|-------|--------|--------|--------|
| `threep` data type | TEXT | DOUBLE ✅ | Convert Jordan's to numeric |
| `plus_minus` data | Empty strings (no data) | INT ✅ | Cannot use for Jordan |
| `age` format | "21-252" (text) | "21-252" (text) | Convert to decimal for both |

**Key Insights from Phase 1:**

- ✅ **LeBron's data imported cleaner** - `threep` and `plus_minus` are already numeric
- ❌ **Plus/minus unavailable for Jordan** - Not tracked during his era (all empty strings)
- ✅ **Playoff data includes `series` and `series_game`** - Enables round-by-round analysis
- ✅ **Game numbering resets each season** - `game` column is 1-82 per season, not a career ID

### Table Relationships

- `jordan_career` ↔ `jordan_playoffs`: Connected by `date` (extract year for season grouping)
- `lebron_career` ↔ `lebron_playoffs`: Connected by `date`
- **No direct season column** - Extract from `date` using `YEAR(date)`
- **Jordan ↔ LeBron**: No direct relationship - compare through aggregated analysis

---

## Phase 2: Analysis Scope Definition

### The 7 Measurable Questions

| # | Question | Metric | Why It Matters |
|---|----------|--------|----------------|
| 1 | Who scores more per game? | Points Per Game (PPG) | Scoring is basketball's primary objective |
| 2 | Who played longer? | Total games, minutes | Longevity shows sustained excellence |
| 3 | Who wins more? | Win percentage | Winning is the ultimate goal |
| 4 | Who is more consistent? | Standard deviation of PPG | Fewer "bad games" = reliability |
| 5 | Who performs better in playoffs? | Playoff PPG - Regular PPG | Big moments define legacies |
| 6 | Who had the higher peak? | Highest single-game points | Ceiling matters |
| 7 | Who contributes more overall? | PTS + AST + TRB per game | Complete players impact more areas |

### Why These 7 Questions?

- ✅ **Simple** - Anyone can understand them
- ✅ **Measurable** - Each maps directly to a SQL calculation
- ✅ **Non-overlapping** - Each captures a unique dimension of greatness
- ✅ **Debate-relevant** - Addresses actual fan arguments

### Greatness Framework

| Category | Jordan Advantage | LeBron Advantage |
|----------|-----------------|------------------|
| Scoring | ✅ Higher PPG | |
| Longevity | | ✅ More games/minutes |
| Winning | ✅ Higher win % | |
| Consistency | | ✅ Lower variance (hypothesis) |
| Playoff Clutch | ✅ Bigger playoff lift (hypothesis) | |
| Peak Performance | ✅ Higher scoring peak | |
| All-Around | | ✅ More PTS+AST+TRB |

*Note: Plus/minus could not be compared due to missing Jordan data.*

**Final Verdict:** The GOAT depends on what you value.

---
## Phase 3: Data Cleaning

### Cleaning Actions Performed

| Issue | Action |
|-------|--------|
| `date` as TEXT | Converted to DATE type |
| `age` as "21-252" TEXT | Converted to DECIMAL (21.69) |
| `result` as "W (+16)" | Extracted win/loss into `is_win` column |
| Jordan `threep` as TEXT | Converted to DOUBLE (empty → 0) |
| Jordan `plus_minus` empty | Set to NULL (no data available) |
| Duplicates | None found |
| Numeric validation | All passed |

### New Cleaned Tables Created

| Table | Rows | Columns |
|-------|------|---------|
| `jordan_career_clean` | 1,042 | 27 |
| `jordan_playoffs_clean` | 177 | 28 |
| `lebron_career_clean` | 1,211 | 27 |
| `lebron_playoffs_clean` | 255 | 28 |

### Key Discovery from Cleaning

**Plus/minus is completely unavailable for Jordan** - this stat was not tracked during his era and cannot be compared.

---

## Phase 4: SQL Analysis & Views (Next)
## Project Structure
