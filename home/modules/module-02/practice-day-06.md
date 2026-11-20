# Practice Day — Stats, pandas, Charts (Day 6)

{% hint style="info" %}
**In one sentence:** No new topics today. You'll practice Days 1–5 and learn to check analysis code that an AI writes for you.
{% endhint %}

## Why this matters

Practicing what you learned a few days ago is what makes it stick. And at work, AI tools will write analysis code for you. The code often runs with no errors and still gives a wrong answer, so you need a routine for checking it.

## What you'll do in class

* Answer two recall questions from memory.
* Follow a classmate-led code-along that uses stats, pandas, and a chart.
* Check a piece of AI-written profiling code. It quietly drops rows, and your job is to catch it.

**Skills:** AI Evaluation · Statistical Analysis · Data Distributions & Shape

## Before you trust AI analysis code

Use this checklist every time an AI writes analysis code for you, in class and in your project:

| Check | Why |
| --- | --- |
| **1. Rows before and after** | A `dropna()` or a filter can remove rows without telling you. |
| **2. One number by hand** | Work out one result yourself and compare it with the code's answer. |
| **3. Data types** | A number column stored as text gives wrong math or errors. |
| **4. What got dropped or filled** | Every removed row or filled-in value changes the answer. Count them. |
| **5. Does the statistic fit the shape?** | An AI may use the mean on skewed data. Look at the chart first. |

## Review: Days 1–5

Try each question before you open the answer.

**1. (Quest 2.1)** When should you report the median instead of the mean?

<details>
<summary>Answer</summary>

When the data is skewed or has big outliers. The median describes a typical value. The mean gets pulled toward the tail.

</details>

**2. (Quest 2.2)** What are the four checks you run on every new file?

<details>
<summary>Answer</summary>

Shape (`df.shape`), data types (`df.dtypes`), missing values (`df.isna().sum()`), and duplicates (`df.duplicated().sum()`).

</details>

**3. (Quest 2.3)** Why keep `count` next to the mean in a `groupby` table?

<details>
<summary>Answer</summary>

So you can see how many rows each average rests on, and spot a group too small to trust.

</details>

**4. (Quest 2.4)** You want to compare the average score across three schools. Which chart?

<details>
<summary>Answer</summary>

A bar chart, one bar per school, with the y-axis starting at zero.

</details>

**5. (Quest 2.5)** Name the two checks you run before you share a chart.

<details>
<summary>Answer</summary>

Where does the y-axis start? Was anything (like an outlier) left out of view?

</details>

## How this connects

* **Data Challenge:** Today finishes "Seattle Weather, Two Tools," where you compare the same work in Python and a spreadsheet.
* **Boss Battle:** In Part 5b, if an AI gives you code, you'll audit it with this same checklist.

---

**Next:** [Quest 2.6 — Drop, Fill, or Flag](quest-06-missing-data.md)
