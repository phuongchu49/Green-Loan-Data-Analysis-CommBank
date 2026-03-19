# 🏦 CommBank Green Loan - Home Mortgage Data Analysis

A data analysis project completed as part of the **Commonwealth Bank You x CommBank Job Simulation (Task 3)**. The goal was to analyse a hypothetical dataset of 500 home mortgage borrowers to identify qualified sales leads for CommBank's **Green Loan** program - a 0.99% p.a. secured loan for renewable energy installations (solar panels, battery storage, EV chargers). Main tool for this project is MS Excel.

Program Task Access: [Green Loan: Data Analysis](https://www.theforage.com/modules/fJYLPoeu5zJ6PCgaM/S76S4mANjKXfDqQkk)

---

## 📋 Project Overview

The Green Loan program is currently available to existing CommBank home mortgage customers. This analysis helps answer:

> *Which borrowers in the market represent the best qualified leads for a Green Loan outreach campaign?*

The analysis moves from broad single-criteria filtering down to a refined set of **110 premium leads** - equity-rich, income-strong homeowners most likely to benefit from and afford the program.

---

## 📂 Dataset

| Property | Detail |
|---|---|
| Source | Hypothetical (not real borrower data) |
| Rows | 500 borrowers |
| Columns | 14 variables |
| Categories | Geographic · Borrower · Mortgage |

**Key columns used in analysis:**

| Column | Variable | Role |
|---|---|---|
| C | % Minority in Local Area | Equity/inclusion filter |
| E | Borrower Annual Income | Affordability filter |
| H | Age of Borrower | Quality/ROI filter |
| I | Borrower Debt-to-Income Ratio | Credit quality filter |
| J | Appraised Value of Home | Investment motivation filter |
| L | LTV Ratio | **Critical - eligibility filter** |

---

## 🛠️ Skills & Tools Used

- **Microsoft Excel** - COUNTIFS, AVERAGE, MIN, MAX, MEDIAN formulas
- **Data bucketing** - grouping continuous variables into meaningful ranges
- **Distribution analysis** - understanding shape of data before filtering
- **Combination/funnel analysis** - stacking criteria to compare volume vs quality
- **Data storytelling** - translating numbers into business recommendations

---

## 🔍 Analysis Approach

The workbook is structured as a **step-by-step walkthrough** across 5 dedicated sheets:

### Step 1 - Orientation
Read every column header and document what it measures, its data type, min/max range, and its relevance to Green Loan qualification. This avoids jumping into formulas without understanding the data first.

### Step 2 - Basic Statistics
Calculate `AVERAGE`, `MIN`, `MAX`, and `MEDIAN` for each key variable.

```excel
=AVERAGE(Sheet1!L8:L507)   → Average LTV across all 500 borrowers
=MIN(Sheet1!E8:E507)        → Lowest annual income in dataset
=MAX(Sheet1!J8:J507)        → Highest appraised home value
```

> Key insight: Wide gaps between MIN and MAX (e.g. income ranges from $18k to $1.56M) signal that averages alone are misleading - distributions are needed.

### Step 3 - Distributions
Use `COUNTIFS` to bucket each variable into ranges and count how many borrowers fall into each group.

```excel
-- Count borrowers with LTV below 60
=COUNTIFS(Sheet1!L8:L507,"<60")

-- Count borrowers with income between $80k and $120k
=COUNTIFS(Sheet1!E8:E507,">=80000",Sheet1!E8:E507,"<120000")

-- Count borrowers in age group "35 to 44" (text match)
=COUNTIFS(Sheet1!H8:H507,"35 to 44")

-- ⚠️ Age brackets with < > symbols need wildcard to avoid numeric comparison:
=COUNTIFS(Sheet1!H8:H507,"*< 25*")
=COUNTIFS(Sheet1!H8:H507,"*> 74*")
```

Five distribution tables were built:
- LTV Ratio distribution
- Annual Income distribution
- Appraised Home Value distribution
- % Minority in Local Area distribution
- Age of Borrower distribution

### Step 4 - Combination Analysis (Funnel)
Stack multiple criteria using `COUNTIFS` with additional condition pairs to find how many borrowers qualify on 2, 3, or 4 criteria simultaneously.

```excel
-- Two criteria: LTV < 80 AND Income > $80k
=COUNTIFS(Sheet1!L8:L507,"<80",Sheet1!E8:E507,">=80000")

-- Three criteria: Financial trifecta
=COUNTIFS(Sheet1!L8:L507,"<80",Sheet1!E8:E507,">=80000",Sheet1!J8:J507,">=400000")

-- Four criteria: Premium leads (recommended target)
=COUNTIFS(Sheet1!L8:L507,"<80",Sheet1!E8:E507,">=80000",Sheet1!J8:J507,">=400000",Sheet1!I8:I507,"<40")
```

This builds a **qualification funnel** showing the trade-off between lead volume and lead quality.

### Step 5 - Key Findings
For each variable and combination, answer three questions:
1. What does the data show?
2. What is the headline number?
3. What does it mean for Green Loan targeting?

---

## 📊 Key Results

### Single Criteria - Maximum Lead Volume

| Criteria | Qualifying Borrowers | % of 500 |
|---|---|---|
| LTV < 80 | 332 | 66.4% |
| Annual Income > $80k | 339 | 67.8% |
| Home Value > $400k | 217 | 43.4% |
| DTI < 40 | 347 | 69.4% |
| % Minority Area > 50% | 85 | 17.0% |
| Age 35–54 | 236 | 47.2% |

### Combination Criteria - Quality Funnel

| Criteria Combination | Leads | % of 500 | Quality |
|---|---|---|---|
| LTV < 80 + Income > $80k | 233 | 46.6% | 🟡 Broad |
| LTV < 80 + Home Value > $400k | 176 | 35.2% | 🟡 Broad |
| LTV < 80 + Income > $80k + Home Value > $400k | 153 | 30.6% | 🟠 High |
| LTV < 80 + Income > $80k + DTI < 40 | 179 | 35.8% | 🟠 High |
| **LTV < 80 + Income > $80k + Home Value > $400k + DTI < 40** | **110** | **22.0%** | **⭐ Premium** |

---

## 🎯 Recommendations

**Primary Target - Financial Leads (110 borrowers)**
Borrowers meeting all 4 financial criteria: equity in their home (LTV < 80), strong income (> $80k), high-value property (> $400k), and manageable existing debt (DTI < 40). These represent the lowest risk and highest likelihood of both qualifying for and benefiting from a Green Loan.

**Secondary Target - Equity/Inclusion Leads (40 borrowers)**
Borrowers in high-minority areas (> 50%) who also hold sufficient equity (LTV < 80) and income (> $80k). Aligned with CommBank's stated commitment to supporting underrepresented communities - a separate, tailored outreach campaign is recommended for this group.

---

## 📁 File Structure

```
📄 Home_Loan_Analysis.xlsx
├── Sheet1                  ← Original raw data (untouched)
├── STEP 1 - Orientation    ← Column guide with data types, ranges & relevance
├── STEP 2 - Basic Stats    ← AVERAGE / MIN / MAX / MEDIAN per key variable
├── STEP 3 - Distributions  ← 5 COUNTIFS distribution tables with % breakdowns
├── STEP 4 - Combinations   ← 4-tier qualification funnel (single → premium)
├── STEP 5 - Key Findings   ← Business interpretation of each finding
└── STEP 6 - Charts         ← Chart data tables + 6 pre-built charts
```

---

## ⚠️ Data Quality Notes

- Dataset is **hypothetical** - not real CommBank borrower data
- Age column (H) stores values as **text brackets** (e.g. `"< 25"`, `"> 74"`) - wildcard COUNTIFS required to avoid Excel interpreting `<` and `>` as numeric operators
- Income distribution is **right-skewed** (a few very high earners pull the average above the median) - median is a more representative central measure for this variable
- Home value and income ranges were **validated against MIN/MAX** after initial formula build - original estimates required correction

---

*Part of the CommBank Unlikely Match Virtual Experience Program - Task 3: Data Analysis*
