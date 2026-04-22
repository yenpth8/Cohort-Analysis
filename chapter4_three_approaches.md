# CHAPTER 4 — How to Build a Cohort Analysis
# Three approaches: Business · Technical (BigQuery + Looker Studio) · Technical (Python)

---

> **PRODUCTION NOTE**
> This chapter is designed to be split across two audiences:
> - **Business audience video:** deliver the Business Approach section only
> - **Technical audience video / follow-up:** deliver Technical Approach Option 1 or 2
> All three approaches follow the same 5-step framework — the steps are identical, only the execution layer changes.

---

---

# ═══════════════════════════════════
# APPROACH A — BUSINESS
# "How to Build a Cohort Analysis (No Code Required)"
# ═══════════════════════════════════

---

*[Face cam. Transition from Chapter 3.]*

Three decisions made. Now the question is: what do you actually *do* with them?

This is the part where most guides hand you a spreadsheet formula and call it a day. We're going to go further — because building a cohort isn't just a technical exercise. It's a five-step thinking process, and the technical part is just Step 3.

Let me walk you through all five.

---

## STEP 1 — Define Your Business Question
*[Slide: Step 1 — Define Your Business Question]*

Everything starts here. Before you open a spreadsheet, before you pull any data — you need one clear sentence that describes what you're trying to find out.

And this is where Decision 1 from the previous chapter comes back in.

*How do you isolate your cohort?* The answer to that question depends entirely on the business question you're asking.

Here are the four types of cohorts most businesses work with, and the questions each one is built to answer:

**Customer cohort.** Groups users by when they first became a customer. Best for: *"Is my overall retention improving over time? Are newer customers staying longer than older ones?"*

**Order cohort.** Groups customers by when they placed their first order. Best for: *"How often do first-time buyers come back? What's the gap between first and second purchase?"* This is the most common starting point for e-commerce businesses.

**Subscription cohort.** Groups users by when they started a subscription. Best for: *"At which month do subscribers typically cancel? Does annual billing retain better than monthly?"*

**Behavioral cohort.** Groups users by a specific action they took — not when they joined. Best for: *"Do users who completed onboarding retain better? Do users who used Feature X stay longer?"* This is the most powerful type for product teams.

*[Pause]*

Write your business question down before moving to Step 2. It should be specific enough that you'll know when you have the answer.

A weak question: *"How is our retention?"*
A strong question: *"Do customers acquired through our referral program retain better at Month 6 than customers from paid social?"*

The stronger your question, the more useful your cohort will be.

---

## STEP 2 — Choose the Right Metric
*[Slide: Step 2 — Choose the Right Metric]*

Your business question from Step 1 determines what you measure.

This step is simpler than it sounds — there are really only three metrics most cohort analyses use:

**Retention rate.** The percentage of a cohort still active at a given time period. This is the default metric for most cohorts and the one we've been discussing throughout this video. Use it when your question is about *who stays*.

**Revenue per cohort.** Instead of tracking whether customers came back, you track how much they spent — period by period. Use it when your question is about *how much they're worth over time*. This gives you LTV curves instead of retention curves.

**Churn rate.** The inverse of retention — the percentage of a cohort that *stopped* being active in each period. Some teams find this easier to act on because it puts the problem front and center. Use it when your question is specifically about *when and how fast you lose people.*

A quick rule: start with retention rate. Once you understand the retention picture, layer in revenue to understand the economic picture. Churn rate is most useful when you're presenting to stakeholders who think in terms of losses rather than percentages retained.

---

## STEP 3 — Create Your Cohort Segment
*[Slide: Step 3 — Create Your Cohort Segment]*

This is where your other two decisions from Chapter 3 come to life.

*What action counts as "active"?* That's your retention event — the behavior that tells you a customer got real value. This becomes the filter for what counts as a return event in your data.

*What time period do you measure?* That determines how you bucket your data — daily, weekly, or monthly windows.

With those two decisions made, creating your cohort segment is three operations:

**Assign each customer to a cohort.** Find each customer's first qualifying event — their first purchase, their first completed trip, their first core feature use. The time period that event falls in is their cohort label. January first purchase → January cohort.

**Log their return events.** For each customer, record every subsequent qualifying event. Every time they came back and did the thing that counts as "active."

**Calculate the period offset.** For each return event, calculate how many periods after the cohort start it occurred. First event = Period 0. One period later = Period 1. Two periods later = Period 2. This is what lets you compare customers across cohorts on the same timeline.

*[Visual: three-column raw data → four-column transformed data with cohort label and period offset added]*

You can do this in Excel or Google Sheets with a few formulas — MINIFS to find the first event date per customer, DATEDIF or a simple subtraction to calculate the period offset. No coding required.

---

## STEP 4 — Visualize with a Cohort Dashboard
*[Slide: Step 4 — Visualize]*

Now you arrange your data into a table and make it readable.

**The cohort table.** Rows represent each cohort — one row per time period. Columns represent time elapsed since acquisition — Period 0, Period 1, Period 2. Each cell shows the retention rate for that cohort at that time period.

*[Visual: cohort table with labeled rows, columns, and one cell highlighted with its formula]*

**Apply conditional formatting.** Color-code the cells on a gradient — deep green for high retention, fading through yellow and orange to red for low retention. This single step transforms a table of numbers into a heatmap your entire team can read in seconds.

**Build retention curves.** Take each row and plot it as a line — X-axis is time elapsed, Y-axis is retention percentage. Overlay multiple cohorts on the same chart. Now you can see immediately whether newer cohorts are tracking above or below older ones, and where the curves flatten.

*[Visual: heatmap → retention curve overlay, side by side]*

These three views — table, heatmap, curve — show you the same data from different angles. The table gives you precision. The heatmap gives you pattern recognition. The curve gives you the story.

---

## STEP 5 — Identify Patterns and Take Action
*[Slide: Step 5 — Identify Patterns → Act]*

This is the step that turns an analysis into a business decision.

There are three directions to read your cohort data, and each one answers a different question:

**Horizontal analysis — read left to right along one row.**
This tells you the story of a single cohort over time. How fast do they drop off? Does the curve flatten, or does it keep declining? Where is the steepest drop? This tells you *when* you're losing people in the customer lifecycle.

**Vertical analysis — read top to bottom down one column.**
This compares different cohorts at the same lifecycle point. "What percentage of each cohort was still active at Month 3?" If the column is getting darker as you go down — your more recent cohorts are retaining better. That's progress. If it's getting lighter — something is getting worse over time.

**Diagonal analysis — read diagonally across the table.**
This shows you what's happening in the real world at a specific calendar point — across all cohorts simultaneously. A diagonal slice represents all customers who were active in, say, October 2024 — regardless of when they joined. If a diagonal suddenly shows a drop, something happened in October that affected everyone: a price change, a bug, a product update, an external shock.

*[Visual: cohort table with three colored arrows — horizontal, vertical, diagonal — each labeled]*

Once you've identified the pattern, the next step is to act on it.

Develop a targeted strategy for the specific cohort or lifecycle point where the problem exists. Then test it — run an A/B test on the next cohort to see if your intervention moves the curve. And keep measuring: use the cohort framework to validate whether what you did actually worked.

The loop is: **Identify → Hypothesize → Intervene → Measure with the next cohort → Repeat.**

---

*[Bridge to Chapter 5:]*

That's the business framework — five steps from question to action. Now, the same five steps look quite different when you're the one actually pulling the data and building the analysis yourself. Let me show you how to do this technically — two ways.

*[Music transition]*

---

---

# ═══════════════════════════════════
# APPROACH B — TECHNICAL OPTION 1
# BigQuery (SQL) → Looker Studio
# ═══════════════════════════════════

---

> **PRODUCTION NOTE**
> Screen recording required throughout. Use a real or realistic synthetic dataset.
> Recommended dataset: e-commerce transaction table with columns: user_id, event_date, event_type
> BigQuery project should be set up before recording.

---

*[Face cam.]*

Same five steps. Now we do them with real tools.

This first technical walkthrough uses **BigQuery** for the data transformation and aggregation, and **Looker Studio** to build the visual. This is the stack most analytics teams at mid-to-large companies are already running — and it scales to tens of millions of rows without breaking a sweat.

Let's go step by step.

---

## STEP 1 — Define Your Business Question
*[Face cam — brief, same as business approach]*

Same as before: write your question before touching anything.

For this walkthrough: *"How does monthly retention compare across customer acquisition cohorts from January to June 2024?"*

That gives us: customer cohort, monthly time period, retention rate metric, and time-based isolation dimension. We're ready.

---

## STEP 2 — Choose the Right Metric

Retention rate. Specifically: the percentage of each monthly cohort still making a purchase in each subsequent month.

Active action: completed purchase. This maps directly to the `event_type = 'purchase'` filter we'll apply in our SQL.

---

## STEP 3 — Data Transformation in BigQuery
*[Screen: BigQuery console, SQL editor open]*

Our raw table is `ecommerce.transactions` with three columns: `user_id`, `event_date`, `event_type`.

We'll build this in two CTEs — Common Table Expressions — which are just named intermediate steps inside one query.

**CTE 1 — Assign each user to their cohort**

```sql
WITH cohort_base AS (
  SELECT
    user_id,
    MIN(DATE_TRUNC(event_date, MONTH)) AS cohort_month
  FROM ecommerce.transactions
  WHERE event_type = 'purchase'
  GROUP BY user_id
),
```

What this does:
- Filters for purchase events only — this is our active action
- Finds each user's *earliest* purchase month using `MIN()`
- `DATE_TRUNC(..., MONTH)` rounds any date to the first of its month — so January 15th and January 28th both become January 1st, which is our cohort label

*[Screen: run CTE 1 in isolation, show result — user_id + cohort_month]*

**CTE 2 — Calculate the period offset for every return event**

```sql
activity AS (
  SELECT
    t.user_id,
    c.cohort_month,
    DATE_TRUNC(t.event_date, MONTH) AS activity_month,
    DATE_DIFF(
      DATE_TRUNC(t.event_date, MONTH),
      c.cohort_month,
      MONTH
    ) AS period_number
  FROM ecommerce.transactions t
  JOIN cohort_base c USING (user_id)
  WHERE t.event_type = 'purchase'
),
```

What this does:
- Joins every purchase event back to the user's cohort month
- `DATE_DIFF(..., MONTH)` calculates how many months after the cohort start each purchase happened
- Period 0 = same month as first purchase. Period 1 = one month later. And so on.

*[Screen: run CTE 2, show result — user_id + cohort_month + activity_month + period_number]*

**Final aggregation — build the cohort table**

```sql
cohort_size AS (
  SELECT
    cohort_month,
    COUNT(DISTINCT user_id) AS total_users
  FROM cohort_base
  GROUP BY cohort_month
)

SELECT
  a.cohort_month,
  a.period_number,
  COUNT(DISTINCT a.user_id)                              AS active_users,
  cs.total_users,
  ROUND(
    COUNT(DISTINCT a.user_id) / cs.total_users * 100, 1
  )                                                      AS retention_rate
FROM activity a
JOIN cohort_size cs USING (cohort_month)
GROUP BY
  a.cohort_month,
  a.period_number,
  cs.total_users
ORDER BY
  a.cohort_month,
  a.period_number
```

What this does:
- Counts distinct active users per cohort per period
- Joins in the total cohort size
- Divides to get retention rate, rounded to one decimal place

*[Screen: run full query, show final result — cohort_month + period_number + active_users + total_users + retention_rate]*

This is the output table. Every row is one cell in the cohort chart — cohort month, period number, and the retention rate for that cell.

**Save this as a view or export to a table:**

```sql
CREATE OR REPLACE VIEW ecommerce.cohort_retention AS
-- [paste full query above]
```

Now Looker Studio can connect to it directly.

---

## STEP 4 — Visualize in Looker Studio
*[Screen: Looker Studio, new report, BigQuery connector]*

Connect your data source: BigQuery → your project → `ecommerce.cohort_retention`.

**Build the pivot table — the cohort heatmap:**

1. Add a **Pivot Table** chart
2. Row dimension: `cohort_month` — format as `MMM YYYY` for readability
3. Column dimension: `period_number`
4. Metric: `retention_rate` — aggregation: Average (or Max, since each cohort/period combination has exactly one row)
5. Apply **conditional formatting** to the metric:
   - Color scale: green (100%) → yellow (~40%) → red (0%)
   - This transforms the table into a heatmap automatically

*[Screen: pivot table appearing with color gradient]*

**Build the retention curve:**

1. Add a **Line Chart**
2. Dimension: `period_number` (X-axis)
3. Breakdown dimension: `cohort_month` (one line per cohort)
4. Metric: `retention_rate`
5. Sort by `period_number` ascending

*[Screen: retention curves appearing — multiple colored lines]*

**Optional — add a summary scorecard:**

Add a **Scorecard** showing average Month 1 retention and average Month 3 retention. These are the two numbers most stakeholders will ask for first.

Your dashboard now has three panels: the heatmap, the curves, and the scorecards. Arrange them so the heatmap is the hero visual at the top.

---

## STEP 5 — Identify Patterns and Take Action

*[Face cam — brief, pointing back to the heatmap on screen]*

Read the same three directions: horizontal for single-cohort lifecycle, vertical for cross-cohort comparison, diagonal for real-world calendar effects.

In Looker Studio, you can add a **date range filter** to let stakeholders slice by cohort month, and a **period filter** to focus on specific lifecycle stages. This makes the dashboard interactive enough for team use — not just a static chart.

When you see an anomaly: right-click on the cell, note the cohort month and period number, and go back to BigQuery. Add a `WHERE cohort_month = '2024-03-01' AND period_number = 2` filter to drill into the individual users in that cell and examine their behavior.

---

---

# ═══════════════════════════════════
# APPROACH B — TECHNICAL OPTION 2
# Python in IDE (pandas + matplotlib / seaborn)
# ═══════════════════════════════════

---

> **PRODUCTION NOTE**
> Use VS Code or JupyterLab — whichever is your default. Jupyter preferred for screen recording because outputs appear inline.
> Required libraries: pandas, numpy, matplotlib, seaborn
> Use same synthetic dataset as BigQuery walkthrough for continuity.

---

*[Face cam.]*

Option 2 is Python — which gives you more flexibility than SQL for exploration, and more control over your visualizations than any BI tool.

This walkthrough uses **pandas** for transformation and aggregation, and **seaborn + matplotlib** for the visual. Same five steps. Same logic. Different syntax.

---

## STEP 1 — Define Your Business Question

Same question: *"How does monthly retention compare across customer acquisition cohorts from January to June 2024?"*

Same active action: completed purchase.
Same metric: retention rate.

---

## STEP 2 — Choose the Right Metric

Retention rate. We'll express it as a percentage and store it in a pivot table — which we'll then pass directly to seaborn's heatmap function.

---

## STEP 3 — Data Transformation in Python
*[Screen: IDE/Jupyter, new notebook or script]*

**Import libraries and load data:**

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as mtick
import seaborn as sns

# Load your data
# Replace with your actual path or database connection
df = pd.read_csv('transactions.csv', parse_dates=['event_date'])

# Keep only purchase events — our active action
df = df[df['event_type'] == 'purchase'].copy()

print(df.head())
print(df.dtypes)
```

*[Screen: show the raw dataframe — user_id, event_date, event_type columns]*

**Step 3a — Assign each user to their cohort month:**

```python
# Find each user's first purchase date
df['cohort_month'] = df.groupby('user_id')['event_date'].transform('min')

# Floor both dates to month start — so Jan 15 and Jan 28 are both "January"
df['cohort_month']   = df['cohort_month'].dt.to_period('M')
df['activity_month'] = df['event_date'].dt.to_period('M')
```

What this does:
- `transform('min')` broadcasts the earliest date back onto every row for that user — so every row knows its user's cohort
- `.dt.to_period('M')` converts timestamps to month periods — `2024-01-15` becomes `2024-01`

*[Screen: show df with two new columns — cohort_month and activity_month]*

**Step 3b — Calculate period offset:**

```python
# Period number = how many months after cohort start each purchase happened
df['period_number'] = (
    df['activity_month'] - df['cohort_month']
).apply(lambda x: x.n)  # .n extracts the integer offset from a Period difference
```

*[Screen: show df with period_number column — 0, 1, 2, 3...]*

**Step 3c — Aggregate into cohort table:**

```python
# Count distinct active users per cohort per period
cohort_data = (
    df.groupby(['cohort_month', 'period_number'])['user_id']
    .nunique()
    .reset_index()
    .rename(columns={'user_id': 'active_users'})
)

# Get total cohort sizes (period 0 = everyone at acquisition)
cohort_size = (
    cohort_data[cohort_data['period_number'] == 0]
    .set_index('cohort_month')['active_users']
    .rename('cohort_size')
)

# Merge cohort size back in and calculate retention rate
cohort_data = cohort_data.join(cohort_size, on='cohort_month')
cohort_data['retention_rate'] = (
    cohort_data['active_users'] / cohort_data['cohort_size'] * 100
).round(1)

print(cohort_data.head(20))
```

*[Screen: show cohort_data — cohort_month + period_number + active_users + cohort_size + retention_rate]*

**Step 3d — EDA checkpoint before visualizing:**

```python
# Quick sanity checks
print("Cohorts:", cohort_data['cohort_month'].nunique())
print("Max period:", cohort_data['period_number'].max())
print("Null check:\n", cohort_data.isnull().sum())
print("\nCohort sizes:\n", cohort_size.sort_index())
```

Check:
- Period 0 retention for every cohort should be exactly 100%
- Cohort sizes should be reasonable — if one cohort has 5 users, exclude it from analysis
- No unexpected NULLs in retention_rate

*[Screen: show output of sanity checks]*

---

## STEP 4 — Visualize in Python
*[Screen: continue in IDE/Jupyter]*

**Pivot to matrix format for the heatmap:**

```python
# Pivot: rows = cohort months, columns = period numbers, values = retention rate
cohort_pivot = cohort_data.pivot_table(
    index='cohort_month',
    columns='period_number',
    values='retention_rate'
)

# Convert index to string for cleaner axis labels
cohort_pivot.index = cohort_pivot.index.astype(str)
```

**Plot 1 — Heatmap (the cohort chart):**

```python
fig, ax = plt.subplots(figsize=(14, 6))

sns.heatmap(
    cohort_pivot,
    annot=True,           # show numbers inside cells
    fmt='.1f',            # one decimal place
    cmap='RdYlGn',        # red → yellow → green
    vmin=0,
    vmax=100,
    linewidths=0.5,
    linecolor='white',
    ax=ax,
    cbar_kws={'label': 'Retention Rate (%)'}
)

ax.set_title('Monthly Cohort Retention Heatmap', fontsize=14, fontweight='bold', pad=16)
ax.set_xlabel('Period (Months Since First Purchase)', fontsize=11)
ax.set_ylabel('Cohort Month', fontsize=11)
ax.xaxis.tick_top()
ax.xaxis.set_label_position('top')

plt.tight_layout()
plt.savefig('cohort_heatmap.png', dpi=150, bbox_inches='tight')
plt.show()
```

*[Screen: heatmap rendering — green-yellow-red gradient with numbers in cells]*

**Plot 2 — Retention curves (line chart):**

```python
fig, ax = plt.subplots(figsize=(12, 5))

for cohort in cohort_pivot.index:
    ax.plot(
        cohort_pivot.columns,
        cohort_pivot.loc[cohort],
        marker='o',
        markersize=4,
        label=cohort,
        linewidth=1.8
    )

ax.yaxis.set_major_formatter(mtick.PercentFormatter())
ax.set_xlabel('Months Since First Purchase', fontsize=11)
ax.set_ylabel('Retention Rate', fontsize=11)
ax.set_title('Retention Curves by Cohort', fontsize=14, fontweight='bold')
ax.legend(title='Cohort', bbox_to_anchor=(1.01, 1), loc='upper left', fontsize=9)
ax.set_ylim(0, 105)
ax.grid(axis='y', alpha=0.3)

plt.tight_layout()
plt.savefig('cohort_curves.png', dpi=150, bbox_inches='tight')
plt.show()
```

*[Screen: retention curve overlay — one line per cohort]*

**Optional Plot 3 — Log scale curves for mature cohort comparison:**

```python
fig, ax = plt.subplots(figsize=(12, 5))

for cohort in cohort_pivot.index:
    ax.plot(
        cohort_pivot.columns,
        cohort_pivot.loc[cohort],
        marker='o',
        markersize=4,
        label=cohort,
        linewidth=1.8
    )

ax.set_yscale('log')
ax.yaxis.set_major_formatter(mtick.PercentFormatter())
ax.set_xlabel('Months Since First Purchase', fontsize=11)
ax.set_ylabel('Retention Rate (log scale)', fontsize=11)
ax.set_title('Retention Curves — Log Scale', fontsize=14, fontweight='bold')
ax.legend(title='Cohort', bbox_to_anchor=(1.01, 1), loc='upper left', fontsize=9)
ax.grid(axis='y', alpha=0.3, which='both')

plt.tight_layout()
plt.savefig('cohort_curves_log.png', dpi=150, bbox_inches='tight')
plt.show()
```

*[Screen: same curves on log scale — small differences in mature periods now clearly visible]*

---

## STEP 5 — Identify Patterns and Take Action
*[Face cam — brief]*

Same three reading directions as the business approach. In Python, the advantage is that you can drill down instantly.

**Horizontal — isolate one cohort:**
```python
print(cohort_pivot.loc['2024-03'])
```

**Vertical — compare all cohorts at one period:**
```python
print(cohort_pivot[2].sort_values(ascending=False))
# Which cohort had the best Month 2 retention?
```

**Diagonal — what was happening in a specific calendar month:**
```python
calendar_month = '2024-05'
mask = cohort_data['activity_month'].astype(str) == calendar_month
print(cohort_data[mask][['cohort_month', 'period_number', 'retention_rate']])
```

When you find an anomaly in the heatmap, drill into the raw transaction data to examine the individual users in that cell:

```python
# Who were the users in the March cohort who returned in Period 2?
anomaly_users = df[
    (df['cohort_month'].astype(str) == '2024-03') &
    (df['period_number'] == 2)
]['user_id'].unique()

# What did they do around that time?
df[df['user_id'].isin(anomaly_users)].sort_values(['user_id', 'event_date'])
```

This is the power of working in code rather than a BI tool — the drill-down is one line away, and the full dataset is always accessible.

---

*[Face cam. Bridge to Chapter 5:]*

Whether you built this in a spreadsheet, in BigQuery, or in Python — you now have the same output: a cohort table, a heatmap, and a set of retention curves.

The next question is: what do they actually mean? How do you read them — and how do you know what's worth acting on?

That's Chapter 5.

*[Music transition]*
