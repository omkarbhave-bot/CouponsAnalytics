# CouponAnalytics — Assignment 5.1 Summary

## Goal
Identify factors that distinguish drivers who **accept** a delivered driving coupon (`Y=1`) vs **do not accept** (`Y=0`) using basic EDA, plots, and acceptance-rate comparisons.

## Data & preparation (from `prompt.ipynb`)
- **Source**: UCI / Mechanical Turk survey of driving scenarios (destination, time, weather, passenger, etc.) and coupon type.
- **Rows**: `12684`
- **Overall acceptance**: `7210 / 12684 = 56.84%`
- **Missing values found**:
  - `car`: 12576
  - `CoffeeHouse`: 217
  - `Restaurant20To50`: 189
  - `CarryAway`: 151
  - `RestaurantLessThan20`: 130
  - `Bar`: 107
- **Duplicates**: 74 rows (identified)
- **Handling**: filled missing values with simple defaults:
  - `car → "NA"`, `CoffeeHouse/Bar/Restaurant* → "never"`, `CarryAway → "0"`

## Key findings

### Bar coupons
- **Acceptance rate (Bar coupons overall)**: **41.00%**
- **Bar visit frequency strongly predicts acceptance**:
  - `<= 3/month`: **37.07%** (n=1818)
  - `> 3/month`: **76.88%** (n=199)
- **Higher-likelihood segments (Bar coupons)**:
  - `>1/mo & age>25`: **69.52%** (n=420) vs **33.50%** (n=1597)
  - `>1/mo & no kids passenger & not Farming/Fishing/Forestry`: **71.32%** (n=551) vs **29.60%** (n=1466)
  - **Meets any of these conditions** (not mutually exclusive): **58.89%** (n=776) vs **29.81%** (n=1241)
    - cond1: `>1/mo & passenger not Kid(s) & not Widowed` → **71.32%** (n=551)
    - cond2: `>1/mo & age < 30` → **72.17%** (n=345)
    - cond3: `Restaurant(<20) >4/mo & income < $50K` → **45.35%** (n=344)
- **Hypothesis**: Bar coupon acceptance is highest among “**social / out-and-about**” drivers—**frequent bar visitors**, **not with kids**, and in **age/lifestyle groups** more likely to stop at a bar.

### Coffee House coupons (independent investigation)
- **Rows**: 3996
- **Acceptance rate (Coffee House overall)**: **49.92%**
- **Passenger context matters (Coffee House)**:
  - `Alone`: **43.79%** (n=2256)
  - `Friend(s)`: **59.69%** (n=1228)
  - `Partner`: **57.05%** (n=305)
  - `Kid(s)`: **48.31%** (n=207)
- **Hypothesis**:
  - Acceptance is **higher when traveling with Friend(s)/Partner** than alone.
  - Acceptance trends **higher earlier in the day** (consistent with coffee use).
  - Overall, acceptance seems driven by **social context + time-of-day convenience**.

## Notebook
See `prompt.ipynb` for the full workflow (missing-data audit, plots, and segment-based acceptance comparisons).