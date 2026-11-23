# Practice Day: Review (Day 6)

**Time:** about 3 minutes (no new reading today)

**EDA workflow:** **Inspect** → Clean → **Explore** → Check → Explain (review) ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

There's no new topic today. You'll practice what you learned in the first five quests, and you'll learn a routine for checking analysis code that an AI writes for you.

**Main takeaway:** AI-written code can run with no errors and still give a wrong answer. Check it before you trust it.

**Why it matters at work:** Practicing something a few days after you learn it is what makes it stick. And at work, AI tools will write analysis code for you, so you need a quick way to check it.

## What you'll do in class

* Answer two recall questions from memory.
* Follow a classmate-led code-along that uses stats, pandas, and a chart.
* Check a piece of AI-written profiling code. It quietly drops rows, and your job is to catch it.

**Skills:** AI Evaluation · Statistical Analysis · Data Distributions & Shape

## Before you trust AI analysis code

Use this checklist every time an AI writes analysis code for you, in class and in the Boss Battle (Module Project):

| Check | Why |
| --- | --- |
| **1. Rows before and after** | A filter, or a step that removes rows with blanks, can drop rows without telling you. |
| **2. One number by hand** | Work out one result yourself and compare it with the code's answer. |
| **3. Data types** | A number column stored as text gives wrong math or errors. |
| **4. What got dropped or filled** | Every removed row or filled-in value changes the answer. Count them. |
| **5. Does the statistic fit the shape?** | An AI may use the mean on skewed data. Look at the chart first. |

## Review: the first five quests

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
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Whenever an AI gives you code, you'll check it with this same checklist before you use its answer.

---

**Next:** [Quest 2.6 — Drop, Fill, or Flag: Missing Data (Day 7)](quest-06-missing-data.md)
