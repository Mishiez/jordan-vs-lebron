# Phase 2: Analysis Scope Definition

## The 7 Measurable Questions

| # | Question | Metric | Why It Matters |
|---|----------|--------|----------------|
| 1 | Who scores more per game? | Points Per Game (PPG) | Scoring is basketball's primary objective |
| 2 | Who played longer? | Total games, total minutes | Longevity shows sustained excellence |
| 3 | Who wins more? | Win percentage | Winning is the ultimate goal |
| 4 | Who is more consistent? | Standard deviation of PPG | Fewer "bad games" = reliability |
| 5 | Who performs better in playoffs? | Playoff PPG - Regular PPG | Big moments define legacies |
| 6 | Who had the higher peak? | Highest single-game points | Ceiling matters |
| 7 | Who contributes more overall? | PTS + AST + TRB per game | Complete players impact more areas |

## Why These 7 Questions

- ✅ **Simple** - Anyone can understand them
- ✅ **Measurable** - Each maps directly to a SQL calculation
- ✅ **Non-overlapping** - Each captures a unique dimension of greatness
- ✅ **Debate-relevant** - Addresses actual fan arguments

## Greatness Framework

| Category | Jordan Advantage | LeBron Advantage |
|----------|-----------------|------------------|
| Scoring | Higher PPG | |
| Longevity | | More games/minutes |
| Winning | Higher win % | |
| Consistency | | Expected lower variance |
| Playoff Clutch | Expected bigger playoff lift | |
| Peak Performance | Higher scoring peak | |
| All-Around | | More PTS+AST+TRB |

## Data Limitations

| Limitation | Impact |
|------------|--------|
| No plus/minus for Jordan | Cannot compare this advanced metric |
| Age needs conversion from "21-252" format | Age-based analysis requires cleaning |
| No direct season column | Must extract year from date |
| Different eras | Context matters in final verdict |

## Final Verdict Approach

The GOAT depends on what you value. This analysis presents the data across 7 categories and lets readers draw their own conclusions.