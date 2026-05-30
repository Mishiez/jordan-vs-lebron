# 🏀 The GOAT Debate: Michael Jordan vs LeBron James
> A data-driven Power BI dashboard comparing two basketball legends across 7 key performance categories.

📊 **7 categories analysed · 2 players · 2,685 games of data · No definitive winner found**

![Dashboard Preview](images/dashboard_page1.png)

---

## Overview

The debate over the greatest basketball player of all time (GOAT) often centres on Michael Jordan and LeBron James. This project uses historical game data to compare both players across seven key categories — not to declare a winner, but to let the data show where each player truly excels.

---

## Key Question

**Who has the stronger statistical case for being considered the GOAT?**

- Who scored more per game?
- Who sustained excellence longer?
- Who contributed more to winning?
- Who performed better under pressure?
- Who had the higher peak?

---

## Dataset

**Source:** Maven Analytics (mavenanalytics.io)

| File | Description |
|------|-------------|
| `jordan_career.csv` | Jordan regular season stats |
| `jordan_playoffs.csv` | Jordan playoff stats |
| `lebron_career.csv` | LeBron regular season stats |
| `lebron_playoffs.csv` | LeBron playoff stats |

**Total games analyzed:** 2,685

---

## Tools Used

- **MySQL** — Data cleaning, transformation, and analysis
- **Microsoft Power BI** — Visualisation and dashboard development
- **DAX** — Custom measures and calculations

---

## Key Findings

### 🔵 Michael Jordan
- Higher career scoring average (30.5 PPG vs 27.3 PPG)
- Higher Finals scoring average
- Strongest playoff scoring lift
- Undefeated in NBA Finals series (6–0)

### 🟡 LeBron James
- Longer career — 1,211 games vs 1,042
- 94 career triple-doubles vs 27
- Greater all-around contribution
- More NBA Finals appearances

### 🤝 Shared Achievement
Both players finished with an **identical 66.1% career win percentage**

---

## Category Summary

| Category | Leader |
|----------|--------|
| Scoring | Jordan |
| Peak Performance | Jordan |
| Finals Dominance | Jordan |
| Career Longevity | LeBron |
| Consistency | LeBron |
| All-Around Impact | LeBron |
| Career Win Rate | Tie |

---

## Dashboard Structure

8-page interactive Power BI report — navigate using page tabs at the bottom.

| Page | Title |
|------|-------|
| 1 | Home — The Setup |
| 2 | Scoring Analysis |
| 3 | Longevity Analysis |
| 4 | Winning Analysis |
| 5 | Consistency Analysis |
| 6 | Playoff Performance |
| 7 | Peak Performance |
| 8 | Final Verdict |

---

## Conclusion

The analysis revealed two different paths to greatness.

**Michael Jordan** excelled in scoring dominance, peak performance, and Finals success.

**LeBron James** excelled in longevity, consistency, and all-around contribution.

> *The data does not identify a single GOAT. The answer depends on which qualities you value most in a player.*

---

## How to Open

1. Download the `.pbix` file
2. Open with **Power BI Desktop** — free at [powerbi.microsoft.com](https://powerbi.microsoft.com)
3. Start at **Page 1** and explore through to **Page 8**

---

## Project Structure
 
```
jordan-vs-lebron/
│
├── GOAT_debate.pbix                        # Power BI dashboard
├── README.md                               # Project documentation
├── .gitignore                              # Git ignore file
│
├── data/
│   └── raw/
│       ├── jordan_career.csv
│       ├── jordan_playoffs.csv
│       ├── lebron_career.csv
│       ├── lebron_playoffs.csv
│       ├── career_data_dictionary.csv
│       └── playoffs_data_dictionary.csv
│
├── images/
│   ├── dashboard_page1.png
│   ├── dashboard_page7.png
│   └── dashboard_page8.png
│
└── docs/
    ├── phase1_data_understanding.md
    ├── phase2_analysis_scope.md
    ├── phase3_data_cleaning.md
    ├── phase4_eda_findings.md
    ├── phase5_advanced_sql_analysis.md
    ├── phase6_reporting_views.md
    ├── phase7_data_modeling_dax.md
    └── phase8_dashboard_development.md
```


---

*Created for educational and portfolio purposes only. Statistics used are for non-commercial analysis.*