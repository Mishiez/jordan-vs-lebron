# jordan-vs-lebron
# 🏀 The GOAT Debate: Jordan vs LeBron - A Data-Driven Analysis

## Project Overview

This project analyzes over 2,500+ career games to answer one of sports' most debated questions: **Who is the greatest basketball player of all time?**

Using **SQL** for data processing and **Power BI** for visualization, this analysis compares Michael Jordan and LeBron James across 7 measurable categories that anyone can understand—no basketball knowledge required.

---

## Phase 1: Dataset Understanding

### Data Sources

The dataset contains game-level statistics for both players' entire careers:

| Table Name | Description | Rows |
|------------|-------------|------|
| `jordan_career` | Michael Jordan - Regular season games | ~1,000+ |
| `jordan_playoffs` | Michael Jordan - Playoff games | ~100+ |
| `lebron_career` | LeBron James - Regular season games | ~1,500+ |
| `lebron_playoffs` | LeBron James - Playoff games | ~200+ |

### Key Columns Discovered

| Column | Meaning | Data Type After Import |
|--------|---------|----------------------|
| `pts` | Points scored in game | INT |
| `ast` | Assists | INT |
| `trb` | Total rebounds | INT |
| `mp` | Minutes played | INT |
| `game_score` | Single-game performance metric | DOUBLE |
| `plus_minus` | Point differential while on court | TEXT (needs cleaning) |
| `threep` | 3-point percentage | TEXT (needs cleaning) |

### Data Quality Findings

During Phase 1, the following inconsistencies were identified:

| Issue | Jordan Career | LeBron Career | Action Needed |
|-------|--------------|---------------|----------------|
| `threep` data type | TEXT | DOUBLE | Clean Jordan's data |
| `plus_minus` data type | TEXT | INT | Clean Jordan's data |
| `age` format | "24-183" (text) | "24-183" (text) | Convert to decimal |

**Key Insight:** LeBron's data imported cleaner than Jordan's, requiring targeted cleaning before comparison.

### Relationships Identified

- `jordan_career` ↔ `jordan_playoffs`: Connected by season/date
- `lebron_career` ↔ `lebron_playoffs`: Connected by season/date
- Playoff tables include additional columns: `series`, `series_game` (allows round-by-round analysis)

---

## Phase 2: Analysis Scope Definition

### The 7 Measurable Questions

Before any data cleaning, the analysis scope was defined to ensure focused, relevant work:

| # | Question | Metric | Why It Matters |
|---|----------|--------|----------------|
| 1 | Who scores more per game? | Points Per Game (PPG) | Scoring is basketball's primary objective |
| 2 | Who played longer? | Total games, minutes, seasons | Longevity shows sustained excellence |
| 3 | Who wins more? | Win percentage | Winning is the ultimate goal |
| 4 | Who is more consistent? | Standard deviation of PPG | Fewer "bad games" = reliability |
| 5 | Who performs better in playoffs? | Playoff PPG - Regular PPG | Big moments define legacies |
| 6 | Who had the higher peak? | Best season PPG | Ceiling matters |
| 7 | Who contributes more overall? | PTS + AST + TRB per game | Complete players impact more areas |

### Why These 7 Questions?

These questions were chosen because they are:

- ✅ **Simple** - Anyone can understand them
- ✅ **Measurable** - Each maps directly to a SQL calculation
- ✅ **Non-overlapping** - Each captures a unique dimension of greatness
- ✅ **Debate-relevant** - Addresses the actual arguments fans make

### Greatness Framework

Rather than forcing a single winner, this project presents a **weighted decision framework**:

| Category | Jordan Advantage | LeBron Advantage |
|----------|-----------------|------------------|
| Scoring | ✅ Higher PPG | |
| Longevity | | ✅ More games/minutes |
| Winning | ✅ Higher win % | |
| Consistency | | ✅ Lower variance |
| Playoff Clutch | ✅ Bigger playoff lift | |
| Peak Performance | ✅ Higher scoring peak | |
| All-Around | | ✅ More PTS+AST+TRB |

**Final Verdict:** The GOAT depends on what you value.

---

## Next Phases

- **Phase 3:** Data Cleaning (targeted to the 7 questions above)
- **Phase 4:** SQL Analysis & Views
- **Phase 5:** Power BI Dashboard
- **Phase 6:** Insights & Recommendations

---

## Tools Used

- **Database:** MySQL / SQL Server
- **Analysis:** SQL (aggregations, window functions, CTEs)
- **Visualization:** Microsoft Power BI
- **Documentation:** GitHub + Markdown

---

## How to Navigate This Repository
