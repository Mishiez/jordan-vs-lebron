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
## Phase 4: Exploratory Data Analysis (EDA)

### Key Discoveries

| Question | Finding |
|----------|---------|
| **Q1: Scoring** | Jordan averages 30.5 PPG (regular) vs LeBron's 27.3. Jordan has 173 games with 40+ points (16.6%) vs LeBron's 65 (5.4%). |
| **Q2: Longevity** | LeBron played 1,211 games (46,619 minutes). Jordan played 1,042 games (40,061 minutes). |
| **Q3: Winning** | Both have identical 66.1% regular season win percentage. Jordan's peak season (87.1%) was higher. |
| **Q4: Consistency** | LeBron has lower scoring variance (StdDev 7.8 vs 9.5) and slightly fewer "bad games" (under 15 points). |
| **Q5: Playoffs** | Jordan rises +3.0 PPG in playoffs (LeBron +1.6). Jordan's Finals win % is 70.6%; LeBron's is 40.7%. |
| **Q6: Peak** | Jordan's highest game: 69 points. LeBron's: 61 points. Jordan's playoff highest: 63; LeBron's: 51. |
| **Q7: All-around** | Combined PTS+AST+TRB is nearly identical (42.0 vs 42.2). Jordan scores more; LeBron assists/rebounds more. |

### The Narrative

> **Jordan was the higher peak scorer and Finals performer. LeBron was more consistent, durable, and well-rounded. Their overall winning percentages are identical. The GOAT depends on what you value.**

### EDA Scoring Distribution

| Points Range | Jordan % | LeBron % |
|--------------|----------|----------|
| 0-9 | 0.7% | 0.5% |
| 10-19 | 11.2% | 15.9% |
| 20-29 | 34.3% | 46.0% |
| 30-39 | 37.2% | 32.3% |
| 40-49 | 13.6% | 4.4% |
| 50+ | 3.0% | 1.0% |

*Detailed EDA findings available in `docs/phase4_eda_findings.md`*

---

## Phase 5: Advanced SQL Analysis (Next)
## Phase 5: Advanced SQL Analysis

### Key Findings by Question

| Question | Winner | Key Stat |
|----------|--------|----------|
| **Q1: Scoring** | Jordan | 30.5 PPG vs LeBron's 27.3 PPG |
| **Q2: Longevity** | LeBron | 1,211 games vs Jordan's 1,042 |
| **Q3: Winning** | Tie | Both 66.1% career win percentage |
| **Q4: Consistency** | LeBron | Std dev 7.8 vs Jordan's 9.5 |
| **Q5: Playoffs** | Jordan | Finals win % 70.6% vs LeBron's 40.7% |
| **Q6: Peak** | Jordan | 35.8 PPG season vs LeBron's 30.4 |
| **Q7: All-Around** | LeBron | 94 triple-doubles vs Jordan's 27 |

### Detailed Insights

**Scoring:**
- Jordan playoff lift: +3.0 PPG | LeBron playoff lift: +1.6 PPG
- Jordan 40+ point games: 173 (16.6%) | LeBron: 65 (5.4%)

**Longevity:**
- LeBron total minutes: 46,619 | Jordan: 40,061 (6,558 more for LeBron)

**Winning:**
- Identical 66.1% win rate - most remarkable finding
- Both perform better vs winning teams (66.6-66.8%) than losing teams (43.8-45.8%)

**Consistency:**
- LeBron typical games (20-30 pts): 50.0% | Jordan: 38.4%
- Jordan great games (40+ pts): 16.6% | LeBron: 5.4%

**Playoffs:**
- Jordan Finals record: 24-10 (70.6%) | LeBron: 22-32 (40.7%)
- LeBron Game 7 PPG: 34.9 | Jordan: 33.7

**Peak:**
- Jordan best 10-game stretch: 38.6 PPG | LeBron: 36.4 PPG
- LeBron peaked at age 21 (30.4 PPG) | Jordan at age 25 (35.8 PPG)

**All-Around:**
- Weighted score (PTS + 1.5AST + 1.2TRB): LeBron 47.4 | Jordan 45.9
- LeBron triple-doubles: 94 (7.8% of games) | Jordan: 27 (2.6%)

### The Verdict

> **Michael Jordan was the superior scorer, peak performer, and Finals winner. LeBron James was more consistent, durable, and all-around. Their career win percentages are identical. The GOAT depends entirely on what you value.**

*Detailed analysis available in `docs/phase5_advanced_sql_analysis.md`*

---

## Phase 6: Creating Views for Power BI (Next)
## Project Structure
