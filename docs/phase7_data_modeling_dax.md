# Phase 7: Data Modeling & DAX

## Overview

This phase created calculated measures, KPIs, dynamic text, and an interactive weighted scoring system in Power BI. All measures are stored in a dedicated `Measures` table for clean organization.

---

## Where Measures Were Created

| Component | Location | Count |
|-----------|----------|-------|
| Lookup Measures | Measures table | 42 |
| Comparison Measures | Measures table | 7 |
| KPI Leader Measures | Measures table | 7 |
| Dynamic Text Measures | Measures table | 7 |
| What-If Parameters | Auto-generated tables | 7 |
| Normalized Scores | Measures table | 14 |
| Weighted GOAT Scores | Measures table | 2 |
| GOAT Decision Measures | Measures table | 2 |
| Calculated Columns | vw_season_ppg, vw_age_analysis | 3 |

---

## Measure Categories

### 1. Lookup Measures (42 measures)

Extract specific values from imported views.

| Example Measure | Source | Value |
|----------------|--------|-------|
| `Jordan PPG Regular` | vw_ppg_comparison | 30.5 |
| `LeBron PPG Regular` | vw_ppg_comparison | 27.3 |
| `Jordan Total Games` | vw_longevity | 1,042 |
| `LeBron Total Games` | vw_longevity | 1,211 |
| `Jordan TripleDoubles` | vw_consistency | 27 |
| `LeBron TripleDoubles` | vw_consistency | 94 |
| `Jordan Finals Win Pct` | vw_finals_performance | 70.6% |
| `LeBron Finals Win Pct` | vw_finals_performance | 40.7% |

### 2. Comparison Measures (7 measures)

Calculate differences between players.

| Measure | Formula | Result |
|---------|---------|--------|
| `PPG Difference` | Jordan PPG - LeBron PPG | 3.2 |
| `Games Difference` | LeBron Games - Jordan Games | 169 |
| `Minutes Difference` | LeBron Minutes - Jordan Minutes | 6,558 |
| `TripleDouble Difference` | LeBron TD - Jordan TD | 67 |
| `Finals Win Pct Difference` | Jordan Finals% - LeBron Finals% | 29.9% |
| `StdDev Difference` | Jordan StdDev - LeBron StdDev | 1.7 |
| `WeightedScore Difference` | LeBron Weighted - Jordan Weighted | 1.5 |

### 3. KPI Leader Measures (7 measures)

Determine who leads each category.

| Measure | Logic | Winner |
|---------|-------|--------|
| `Scoring Leader` | Higher PPG | Jordan |
| `Longevity Leader` | More games | LeBron |
| `Winning Leader` | Higher win % | Tie |
| `Consistency Leader` | Lower std dev | LeBron |
| `Playoff Leader` | Higher Finals win % | Jordan |
| `Peak Leader` | Higher scoring game | Jordan |
| `AllAround Leader` | More triple-doubles | LeBron |

### 4. Dynamic Text Measures (7 measures)

Generate human-readable sentences.

| Measure | Example Output |
|---------|----------------|
| `Scoring Leader Text` | "Jordan leads scoring by 3.2 points per game" |
| `Longevity Leader Text` | "LeBron played 169 more games and 6,558 more minutes" |
| `Playoff Leader Text` | "Jordan wins 70.6% of Finals games. LeBron wins 40.7%." |
| `Consistency Leader Text` | "LeBron's standard deviation is 7.8 vs Jordan's 9.5" |
| `AllAround Leader Text` | "LeBron has 94 triple-doubles (7.76% of games)" |
| `Peak Leader Text` | "Jordan's highest game is 69 points vs LeBron's 61" |
| `Overall Verdict Text` | Summary sentence of all findings |

### 5. What-If Parameters (7 parameters)

User-controlled sliders for weighted GOAT score.

| Parameter | Min | Max | Default | Purpose |
|-----------|-----|-----|---------|---------|
| `Weight_Scoring` | 0 | 100 | 14 | How much scoring matters |
| `Weight_Longevity` | 0 | 100 | 14 | How much longevity matters |
| `Weight_Winning` | 0 | 100 | 14 | How much winning matters |
| `Weight_Consistency` | 0 | 100 | 14 | How much consistency matters |
| `Weight_Playoffs` | 0 | 100 | 15 | How much playoffs matter |
| `Weight_Peak` | 0 | 100 | 15 | How much peak matters |
| `Weight_AllAround` | 0 | 100 | 14 | How much all-around matters |

### 6. Normalized Scores (14 measures)

Convert raw stats to 0-10 scale per category.

| Measure | Formula Logic |
|---------|---------------|
| `Jordan Score Scoring` | If higher PPG than LeBron → 10, else (Jordan PPG/LeBron PPG)×10 |
| `LeBron Score Scoring` | If higher PPG than Jordan → 10, else (LeBron PPG/Jordan PPG)×10 |
| `Jordan Score Longevity` | Based on games played comparison |
| `LeBron Score Longevity` | Based on games played comparison |
| `Jordan Score Winning` | Always 10 (both 66.1%) |
| `LeBron Score Winning` | Always 10 |
| `Jordan Score Consistency` | Based on lower standard deviation |
| `LeBron Score Consistency` | Based on lower standard deviation |
| `Jordan Score Playoffs` | Based on Finals win % |
| `LeBron Score Playoffs` | Based on Finals win % |
| `Jordan Score Peak` | Based on highest scoring game |
| `LeBron Score Peak` | Based on highest scoring game |
| `Jordan Score AllAround` | Based on triple-doubles |
| `LeBron Score AllAround` | Based on triple-doubles |

### 7. Weighted GOAT Scores (2 measures)

Multiply normalized scores by user weights and sum.

| Measure | Formula |
|---------|---------|
| `Jordan Weighted GOAT Score` | Sum of (Jordan Score × Weight) for all 7 categories |
| `LeBron Weighted GOAT Score` | Sum of (LeBron Score × Weight) for all 7 categories |

### 8. GOAT Decision Measures (2 measures)

Determine winner based on weighted scores.

| Measure | Output |
|---------|--------|
| `GOAT Winner` | "Jordan", "LeBron", or "Tie" |
| `GOAT Verdict Text` | Dynamic sentence like "With your weights, Jordan is the GOAT (345 vs 328)" |

### 9. Calculated Columns (3 columns)

Added directly to existing tables.

| Column | Table | Purpose |
|--------|-------|---------|
| `Season Label` | vw_season_ppg | Format season as "1987-88" for better chart labels |
| `Decade` | vw_season_ppg | Group seasons into 1980s, 1990s, 2000s, etc. |
| `Age Group` | vw_age_analysis | Group ages into Early Career, Prime, etc. |

---

## Key DAX Patterns Used

### Pattern 1: Lookup Measure

```dax
Measure Name = 
CALCULATE(
    AVERAGE(table[column]),
    table[filter_column] = "filter_value"
)```

### Pattern 2: Comparison Measure
```dax
Difference = [Measure A] - [Measure B]
```
### Pattern 3: KPI Leader
```dax
Leader = 
IF(
    [Measure A] > [Measure B],
    "Player A",
    IF([Measure B] > [Measure A], "Player B", "Tie")
)```

### Pattern 4: Dynamic Text
dax
Text = 
"Player A leads by " & FORMAT([Difference], "0.0") & " units"
### Pattern 5: Normalized Score
``` dax
Normalized Score = 
VAR JordanValue = [Jordan Measure]
VAR LeBronValue = [LeBron Measure]
VAR MaxValue = MAX(JordanValue, LeBronValue)
RETURN
IF(
    MaxValue = JordanValue,
    10,
    (JordanValue / LeBronValue) * 10
)```

### Pattern 6: Weighted Score
```dax
Weighted Score = 
([Score1] * [Weight1 Value]) +
([Score2] * [Weight2 Value]) +
...```

