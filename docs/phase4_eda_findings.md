# Phase 4: Exploratory Data Analysis (EDA) Findings

## Overview

This phase explored the cleaned data to understand distributions, ranges, and patterns before formal analysis. All 7 questions were examined using basic SQL (aggregations, groupings, distributions).

---

## Question 1: Who scores more per game?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Regular Season PPG | **30.5** | 27.3 |
| Playoff PPG | **33.5** | 28.9 |
| Playoff Lift | **+3.0** | +1.6 |
| 40+ Point Games | **173 (16.6%)** | 65 (5.4%) |
| 50+ Point Games | **31** | 12 |
| Sub-10 Point Games | 7 (0.7%) | 6 (0.5%) |

### Scoring Distribution

| Points Range | Jordan Games | Jordan % | LeBron Games | LeBron % |
|--------------|-------------|----------|--------------|----------|
| 0-9 | 7 | 0.7% | 6 | 0.5% |
| 10-19 | 117 | 11.2% | 192 | 15.9% |
| 20-29 | 357 | 34.3% | 557 | 46.0% |
| 30-39 | 388 | 37.2% | 391 | 32.3% |
| 40-49 | 142 | 13.6% | 53 | 4.4% |
| 50+ | 31 | 3.0% | 12 | 1.0% |

### Discovery

Jordan is a significantly more prolific scorer, especially in high-scoring games (40+, 50+). He has nearly 3 times as many 40+ point games as LeBron. However, LeBron has a tighter scoring distribution with more games in the 20-29 range.

---

## Question 2: Who played longer?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Total Games | 1,042 | **1,211** |
| Total Minutes | 40,061 | **46,619** |
| Avg Minutes/Game | 38.4 | 38.5 |
| 40+ Minute Games | 488 (46.8%) | 497 (41.0%) |

### Minutes Distribution

| Minutes Range | Jordan Games | Jordan % | LeBron Games | LeBron % |
|---------------|-------------|----------|--------------|----------|
| Under 20 | 8 | 0.8% | 3 | 0.2% |
| 20-29 | 61 | 5.9% | 53 | 4.4% |
| 30-39 | 462 | 44.3% | 625 | 51.6% |
| 40-47 | 488 | 46.8% | 497 | 41.0% |
| 48+ (OT) | 23 | 2.2% | 33 | 2.7% |

### Discovery

LeBron has significantly more career mileage: 169 more games and 6,558 more minutes (equivalent to about 136 additional full games). Jordan played a higher percentage of "heavy workload" games (40+ minutes).

---

## Question 3: Who wins more?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Regular Season Win % | 66.1% | 66.1% |
| Playoff Win % | 66.7% | 66.3% |
| Peak Season Win % | **87.1% (1996)** | 81.2% (2013) |
| Lowest Season Win % | 45.3% (1985) | 25.9% (2003) |

### Jordan Win % by Season

| Season | Win % | Season | Win % |
|--------|-------|--------|-------|
| 1996 | 87.1% | 1992 | 81.3% |
| 1997 | 75.6% | 1991 | 80.2% |
| 1998 | 80.8% | 1995 | 84.4% |

### LeBron Win % by Season

| Season | Win % | Season | Win % |
|--------|-------|--------|-------|
| 2013 | 81.2% | 2016 | 80.6% |
| 2010 | 78.0% | 2009 | 78.0% |
| 2008 | 70.1% | 2012 | 70.9% |

### Discovery

Overall winning percentages are nearly identical. Jordan's peak seasons were more dominant (87.1% vs 81.2%). LeBron carried much weaker early teams (25.9% win rate as a rookie).

---

## Question 4: Who is more consistent?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Standard Deviation (PPG) | 9.5 | **7.8** |
| Games Under 15 Points | 43 (4.1%) | **46 (3.8%)** |
| Games Over 40 Points | **173 (16.6%)** | 65 (5.4%) |

### Discovery

This reveals the fundamental difference between the two players:
- **LeBron is more consistent** - lower variance, fewer "bad games" relative to total
- **Jordan has higher peaks** - far more dominant scoring games

This trade-off is central to the GOAT debate: consistency vs peak dominance.

---

## Question 5: Who performs better in playoffs?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Playoff PPG vs Regular | **+3.0** | +1.6 |
| Playoff Win % | 66.7% | 66.3% |
| Finals Win % | **70.6% (24-10)** | 40.7% (22-32) |
| First Round Win % | 66.7% | **83.9%** |

### Jordan Playoff Win % by Round

| Round | Games | Win % |
|-------|-------|-------|
| EC1 (First Round) | 45 | 66.7% |
| ECS (Semifinals) | 53 | 66.0% |
| ECF (Conf Finals) | 45 | 64.4% |
| FIN (Finals) | 34 | **70.6%** |

### LeBron Playoff Win % by Round

| Round | Games | Win % |
|-------|-------|-------|
| EC1 (First Round) | 62 | **83.9%** |
| ECS (Semifinals) | 67 | 68.7% |
| ECF (Conf Finals) | 57 | 64.9% |
| FIN (Finals) | 54 | 40.7% |

### Discovery

The biggest separation is in the **Finals**. Jordan won 70.6% of his Finals games; LeBron won 40.7%. However, LeBron dominates earlier rounds (83.9% in first round), suggesting his teams were often favored but faced tougher Finals competition.

---

## Question 6: Who had the higher peak?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Highest Scoring Game | **69 points** | 61 points |
| 60+ Point Games | **2** | 1 |
| Playoff Highest | **63 points** | 51 points |
| Top 5 Playoff Scores | 63, 56, 55, 55, 55 | 51, 49, 49, 48, 47 |

### Jordan's Top 5 Regular Season Games

| Date | Opponent | Points | Result |
|------|----------|--------|--------|
| 1990-03-28 | CLE | 69 | Win |
| 1993-01-16 | ORL | 64 | Loss |
| 1987-03-04 | DET | 61 | Win |
| 1987-04-16 | ATL | 61 | Loss |
| 1988-04-03 | DET | 59 | Win |

### LeBron's Top 5 Regular Season Games

| Date | Opponent | Points | Result |
|------|----------|--------|--------|
| 2014-03-03 | CHA | 61 | Win |
| 2017-11-03 | WAS | 57 | Win |
| 2005-03-20 | TOR | 56 | Loss |
| 2009-02-20 | MIL | 55 | Win |
| 2005-12-10 | MIL | 52 | Loss |

### Discovery

Jordan's scoring peak is undeniably higher: 69 vs 61 in regular season, 63 vs 51 in playoffs. His top 5 playoff scores (63, 56, 55, 55, 55) far exceed LeBron's (51, 49, 49, 48, 47).

---

## Question 7: Who contributes more overall?

### Key Findings

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Avg Combined (PTS+AST+TRB) | 42.0 | **42.2** |
| Avg Points | **30.5** | 27.3 |
| Avg Assists | 5.3 | **7.4** |
| Avg Rebounds | 6.3 | **7.5** |
| Combined 50+ Games | **261 (25.0%)** | 241 (19.9%) |

### Combined Score Distribution

| Combined Range | Jordan Games | Jordan % | LeBron Games | LeBron % |
|----------------|-------------|----------|--------------|----------|
| Under 20 | 21 | 2.0% | 8 | 0.7% |
| 20-29 | 100 | 9.6% | 95 | 7.8% |
| 30-39 | 304 | 29.2% | 362 | 29.9% |
| 40-49 | 356 | 34.2% | 505 | 41.7% |
| 50+ | 261 | 25.0% | 241 | 19.9% |

### Discovery

Their total combined contribution (PTS+AST+TRB) is nearly identical (42.0 vs 42.2). They achieve it differently: Jordan through scoring, LeBron through balanced assists and rebounds. Jordan has more "elite" combined games (50+), but LeBron is more consistently in the 40-49 range.

---

## Overall EDA Summary

| Question | Jordan Advantage | LeBron Advantage | Tie |
|----------|-----------------|------------------|-----|
| Q1: Scoring | ✅ Higher PPG, more 40+/50+ games | More consistent scoring | |
| Q2: Longevity | | ✅ More games, minutes | |
| Q3: Winning | Peak season dominance | | ✅ Overall win % identical |
| Q4: Consistency | | ✅ Lower variance, fewer bad games | |
| Q5: Playoffs | ✅ Finals performance, higher lift | First round dominance | Overall win % tie |
| Q6: Peak | ✅ Higher scoring games | | |
| Q7: All-around | | ✅ Better assists/rebounds | ✅ Combined total identical |

---

## The Narrative

> **Jordan was the higher peak scorer and Finals performer. LeBron was more consistent, durable, and well-rounded. Their overall winning percentages are identical. The GOAT depends on what you value.**

---

## Next Steps

Proceed to **Phase 5: Advanced SQL Analysis** to definitively answer each question using CTEs, window functions, and joins.