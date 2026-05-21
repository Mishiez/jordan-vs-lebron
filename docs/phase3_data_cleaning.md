# Phase 3: Data Cleaning

## Overview

This phase focused on preparing the raw data for analysis by:
1. Checking for missing values
2. Standardizing data types
3. Removing duplicates
4. Validating numeric columns

All cleaning was performed using SQL in MySQL Workbench.

---

## Step 1: Check for Missing Values

### Approach

We checked for both NULL values AND empty strings (`''`), as Jordan's data contained empty strings in several columns.

### Findings

| Table | Column | Missing Count | Total Rows | % Missing | Action |
|-------|--------|--------------|------------|-----------|--------|
| jordan_career | `plus_minus` | 1,042 | 1,042 | 100% | Set to NULL (no data available) |
| jordan_career | `threep` | 314 | 1,042 | 30% | Convert empty to 0 (no 3-point attempts) |
| jordan_playoffs | `plus_minus` | 177 | 177 | 100% | Set to NULL (no data available) |
| jordan_playoffs | `threep` | 33 | 177 | 19% | Convert empty to 0 |
| lebron_career | `threep` | 319 | 1,211 | 26% | Convert NULL to 0 |
| lebron_career | `plus_minus` | 27 | 1,211 | 2% | Keep as NULL |
| lebron_playoffs | `threep` | 55 | 255 | 22% | Convert NULL to 0 |
| lebron_playoffs | `plus_minus` | 6 | 255 | 2% | Keep as NULL |

### Key Discovery

**Plus/minus is completely unavailable for Jordan.** This stat was not tracked during his era. All cross-player comparisons involving plus/minus are impossible.

---

## Step 2: Standardize Data Types

### Changes Made

| Column | Original Type | Target Type | Tables Affected |
|--------|--------------|-------------|-----------------|
| `date` | TEXT | DATE | All 4 tables |
| `age` | TEXT ("21-252") | DECIMAL (21.69) | Career tables only |
| `result` | TEXT ("W (+16)") | Extracted `is_win` (TINYINT) | All 4 tables |
| `threep` (Jordan) | TEXT | DOUBLE | Jordan career + playoffs |
| `threep` (LeBron) | DOUBLE | DOUBLE (no change) | LeBron career + playoffs |
| `plus_minus` (Jordan) | TEXT (empty) | NULL | Jordan career + playoffs |
| `plus_minus` (LeBron) | INT | INT (no change) | LeBron career + playoffs |

### Conversion Logic

#### Age Conversion

#### Win/Loss Extraction

#### 3-Point Percentage


---

## Step 3: Remove Duplicates

### Method

We checked for duplicates using three approaches:

1. **Logical duplicates** - Same date + team + opponent
2. **Game number duplicates** - Same game number + date within same season
3. **Exact row duplicates** - All columns identical

### Results

| Table | Duplicates Found |
|-------|------------------|
| jordan_career | 0 |
| jordan_playoffs | 0 |
| lebron_career | 0 |
| lebron_playoffs | 0 |

**Conclusion:** No duplicate records exist in any table.

---

## Step 4: Validate Numeric Columns

### Validation Checks Performed

| Check | What We Looked For | Acceptable Range |
|-------|-------------------|------------------|
| Negative values | Any column < 0 | 0 minimum |
| Points | pts | 0-100 |
| Minutes | mp | 0-70 (with OT) |
| Made > Attempted | fg > fga, three > threeatt, ft > fta | None allowed |
| Percentages | fgp, ftp, threep | 0-1 |
| Zero minutes with points | mp = 0 AND pts > 0 | None allowed |

### Results

All validation checks passed with zero violations.

---

## Step 5: Create Cleaned Tables

### New Tables Created

| Table Name | Source | Rows | Columns |
|------------|--------|------|---------|
| `jordan_career_clean` | jordan_career | 1,042 | 27 |
| `jordan_playoffs_clean` | jordan_playoffs | 177 | 28 |
| `lebron_career_clean` | lebron_career | 1,211 | 27 |
| `lebron_playoffs_clean` | lebron_playoffs | 255 | 28 |

### New Columns Added

| Column | Type | Description |
|--------|------|-------------|
| `game_date` | DATE | Converted from `date` column |
| `age_decimal` | DECIMAL(5,2) | Converted from `age` column |
| `is_win` | TINYINT | Extracted from `result` (1=Win, 0=Loss) |
| `three_pct` | DOUBLE | Renamed from `threep` for consistency |
| `original_result` | TEXT | Preserved original result for reference |

### Columns Removed or Modified

| Original Column | Action |
|-----------------|--------|
| `date` | Replaced by `game_date` |
| `age` | Replaced by `age_decimal` |
| `threep` | Renamed to `three_pct` |
| `plus_minus` (Jordan) | Set to NULL (no data) |

---

## Verification Results

### Row Count Verification

| Table | Original Rows | Cleaned Rows | Match |
|-------|--------------|--------------|-------|
| jordan_career | 1,042 | 1,042 | ✅ |
| jordan_playoffs | 177 | 177 | ✅ |
| lebron_career | 1,211 | 1,211 | ✅ |
| lebron_playoffs | 255 | 255 | ✅ |

### Data Type Verification

All cleaned tables now have correct data types:
- `game_date` → DATE
- `age_decimal` → DECIMAL
- `is_win` → TINYINT
- `three_pct` → DOUBLE
- All counting stats → INT
- All percentages → DOUBLE

---

## Limitations Documented

| Limitation | Impact on Analysis |
|------------|-------------------|
| No plus/minus for Jordan | Cannot compare this advanced metric |
| 3-point percentage set to 0 for games with no attempts | Assumes 0% is appropriate (debatable but standard) |
| Different eras (pace, rules, 3-point line) | Context matters in final interpretation |

---

## SQL Code Reference

All cleaning queries are available in:
`/sql/02_clean_data.sql`

---

## Phase 3 Summary

| Task | Status |
|------|--------|
| Missing values checked | ✅ Complete |
| Data types standardized | ✅ Complete |
| Duplicates removed | ✅ None found |
| Numeric columns validated | ✅ All passed |
| Cleaned tables created | ✅ Complete |
| Limitations documented | ✅ Complete |

**Ready for Phase 4: SQL Analysis & Views**