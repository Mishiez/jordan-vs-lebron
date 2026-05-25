# Phase 5: Advanced SQL Analysis

## Overview

This phase used advanced SQL techniques (CTEs, window functions, JOINs, subqueries) to definitively answer each of the 7 questions. Unlike EDA which identified patterns, this phase produced exact, quantifiable answers.

### Techniques Used

| Technique | Purpose | Questions |
|-----------|---------|-----------|
| CTEs (WITH clause) | Break complex queries into steps | All |
| Window Functions | Rolling averages, running totals, rankings | Q1, Q2, Q4, Q6 |
| JOINs | Combine career + playoff tables | Q5 |
| CASE statements | Conditional aggregation | Q3, Q5, Q7 |
| RANK() / ROW_NUMBER() | Top performances, peak identification | Q6 |
| Rolling windows (ROWS BETWEEN) | Moving averages over N games | Q1, Q4, Q6 |

---

## Question 1: Who scores more per game?

### Query Results

| Player | Regular PPG | Playoff PPG | Playoff Lift |
|--------|-------------|-------------|--------------|
| Jordan | 30.5 | 33.5 | **+3.0** |
| LeBron | 27.3 | 28.9 | +1.6 |

### Rolling 10-Game Average (Sample)

Jordan's rolling average showed consistency around 27-28 PPG early in his career, with peaks above 35 PPG during hot streaks.

### Season-by-Season Comparison

| Season | Jordan PPG | LeBron PPG |
|--------|-----------|-----------|
| 1988 | 35.8 | - |
| 1990 | 32.8 | - |
| 2006 | - | 30.4 |
| 2008 | - | 29.9 |

### Key Findings

- Jordan averages **3.2 more points per game** in regular season
- Jordan's playoff lift (+3.0) is nearly double LeBron's (+1.6)
- Jordan's best season (35.8 PPG) exceeds LeBron's best (30.4 PPG) by 5.4 points

---

## Question 2: Who played longer?

### Query Results

| Player | Total Games | Total Minutes | Peak Avg Minutes/Season |
|--------|-------------|---------------|------------------------|
| Jordan | 1,042 | 40,061 | 40.7 (1988) |
| LeBron | **1,211** | **46,619** | **42.7 (2005)** |

### Cumulative Minutes Progression

Jordan reached 40,000 minutes over 1,042 games. LeBron surpassed this at approximately game 1,050.

### Season-by-Season Workload

| Season | Jordan Minutes | LeBron Minutes |
|--------|---------------|----------------|
| Age 22-25 | 3,200-3,300 | 3,300-3,400 |
| Age 30-35 | 3,000-3,200 | 2,800-3,000 |

### Key Findings

- LeBron played **169 more games** (equivalent to 2+ full seasons)
- LeBron played **6,558 more minutes** (equivalent to 136 additional full games)
- LeBron's peak workload (42.7 MPG in 2005) exceeded Jordan's (40.7 MPG in 1988)

---

## Question 3: Who wins more?

### Query Results

| Player | Overall Win % | vs Above .500 | vs Below .500 |
|--------|--------------|---------------|---------------|
| Jordan | 66.1% | 66.6% | 45.8% |
| LeBron | 66.1% | 66.8% | 43.8% |

| Player | Home Win % | Away Win % |
|--------|-----------|-----------|
| Jordan | 66.1% | 66.1% |
| LeBron | 66.1% | 66.1% |

### Key Findings

- **Identical overall win percentage (66.1%)** - most remarkable finding
- Both perform significantly better against winning teams
- No home/away advantage difference between players
- LeBron's early career losing seasons (25.9% win rate as rookie) lowered his overall, but he caught up

---

## Question 4: Who is more consistent?

### Query Results

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Standard Deviation (PPG) | 9.5 | **7.8** |
| % Bad Games (<15 pts) | 4.1% | **3.8%** |
| % Great Games (>40 pts) | **16.6%** | 5.4% |
| % Typical Games (20-30 pts) | 38.4% | **50.0%** |
| Consistency Score (custom) | 3.4 | **4.6** |
| Longest 30+ Point Streak | **11 games** | 10 games |

### Rolling 10-Game Standard Deviation

Jordan's rolling std dev fluctuated between 5-12 points throughout his career. LeBron's remained consistently between 6-9 points.

### Key Findings

- LeBron is **significantly more consistent** (lower variance, more typical games)
- Jordan has **dramatically more great games** (3x as many 40+ point games)
- Trade-off: consistency vs peak dominance is the fundamental difference between them

---

## Question 5: Who performs better in playoffs?

### Query Results

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Playoff Lift (Career) | **+3.0** | +1.6 |
| Best Playoff Lift Season | +11.5 (1986) | +6.8 (2018) |
| Game 6 PPG | 31.3 | 29.5 |
| Game 7 PPG | 33.7 | **34.9** |
| Finals Win % | **70.6% (24-10)** | 40.7% (22-32) |
| Finals PPG | **33.9** | 28.6 |

### Playoff Lift by Season

Jordan's largest lift came in 1986 (+11.5 PPG) when he averaged 43.7 PPG in playoffs vs 32.1 in regular season. LeBron's largest lift was 2018 (+6.8 PPG).

### Key Findings

- Jordan rises more in playoffs overall
- LeBron actually averages **more in Game 7s** (34.9 vs 33.7)
- **Finals performance is the biggest separation** - Jordan wins 70.6% of Finals games, LeBron 40.7%
- LeBron dominates first round (83.9% win rate) but struggles in Finals

---

## Question 6: Who had the higher peak?

### Query Results

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Best 10-Game Stretch PPG | **38.6** | 36.4 |
| Peak Season PPG | **35.8 (age 24-25)** | 30.4 (age 21) |
| Top 3 Seasons PPG | 35.8, 35.5, 33.2 | 30.4, 29.9, 29.5 |
| Peak Scoring Age | 24-25 | 21 |

### Age-Based Scoring Comparison

| Age | Jordan PPG | LeBron PPG |
|-----|-----------|-----------|
| 21 | 28.1 | **30.4** |
| 23 | **33.6** | 29.8 |
| 24 | **34.7** | 29.1 |
| 25 | **35.8** | 28.0 |
| 28 | 30.8 | 27.1 |

### Key Findings

- **Jordan's peak scoring is higher** (35.8 vs 30.4)
- **LeBron peaked earlier** (age 21 vs age 25 for Jordan)
- Jordan maintained elite scoring (32+ PPG) from ages 23-30
- LeBron's scoring declined after age 21

---

## Question 7: Who contributes more overall?

### Query Results

| Metric | Jordan | LeBron |
|--------|--------|--------|
| Raw Combined (PTS+AST+TRB) | 42.0 | **42.2** |
| Weighted Score (PTS + 1.5AST + 1.2TRB) | 45.9 | **47.4** |
| Triple-Doubles | 27 (2.6%) | **94 (7.8%)** |
| Age 22-30 Combined Leader | **Jordan** | LeBron |
| Age 32-35 Combined Leader | - | **LeBron** |

### Age-Based Combined Comparison

| Age | Jordan Combined | LeBron Combined | Better At Age |
|-----|----------------|----------------|---------------|
| 22 | 42.3 | 41.4 | Jordan |
| 24 | 46.3 | 44.5 | Jordan |
| 28 | 42.5 | 41.5 | Jordan |
| 32 | 40.9 | 45.0 | LeBron |
| 34 | 38.7 | 44.8 | LeBron |

### Key Findings

- Raw combined total is **nearly identical** (42.0 vs 42.2)
- When weighted for assists and rebounds, LeBron has a clear edge (47.4 vs 45.9)
- LeBron has **3.5x more triple-doubles** (94 vs 27)
- Jordan was better in his 20s; LeBron better in his 30s

---

## Overall Summary Table

| Question | Winner | Margin / Key Finding |
|----------|--------|---------------------|
| Q1: Scoring | **Jordan** | +3.2 PPG regular, +4.6 PPG playoffs |
| Q2: Longevity | **LeBron** | +169 games, +6,558 minutes |
| Q3: Winning | **Tie** | Both 66.1% overall |
| Q4: Consistency | **LeBron** | Std dev 7.8 vs 9.5, 3x fewer great games |
| Q5: Playoffs | **Jordan** | Finals win % 70.6% vs 40.7% |
| Q6: Peak | **Jordan** | 35.8 PPG vs 30.4 PPG peak season |
| Q7: All-Around | **LeBron** | 94 vs 27 triple-doubles |

---

## The Final Narrative

> **Michael Jordan was the superior scorer, peak performer, and Finals winner. LeBron James was more consistent, durable, and all-around. Their career win percentages are identical. The GOAT depends entirely on what you value.**

---

## Next Steps

Proceed to **Phase 6: Creating Views for Power BI** to store these results in reusable views for dashboarding.