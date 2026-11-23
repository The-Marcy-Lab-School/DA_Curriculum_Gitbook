# Practice Day: Review (Day 6)

**Time:** about 3 minutes (no new reading today)

**EDA workflow:** **Inspect** → Clean → **Explore** → Check → Explain (review) ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

There's no new topic today. You'll practice what you learned in the first five quests, and you'll learn a routine for checking analysis code that an AI (artificial intelligence) tool writes for you.

**Main takeaway:** AI-written code can run with no errors and still give a wrong answer. Check it before you trust it.

**Why it matters at work:** Practicing something a few days after you learn it is what makes it stick. And at work, AI tools will write analysis code for you, so you need a quick way to check it.

## What you'll do in class

* Answer three recall questions from memory. One of them is from Module 1.
* Follow a classmate-led code-along that uses stats (statistics), pandas, and a chart. In a **code-along**, everyone writes the same code together, step by step.
* Check a piece of AI-written profiling code (code that sums up what's in a table). It quietly drops rows, and your job is to catch it.

**Skills:** AI Evaluation · Statistical Analysis · Data Distributions & Shape

## Before you trust AI analysis code

You learned the rule behind this checklist in [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md). If AI-written code runs, that only means there was no error. The answer can still be wrong.

Use this checklist every time an AI writes analysis code for you, in class and in the Boss Battle (Module Project):

| Check | Why |
| --- | --- |
| **1. Rows before and after** | A filter, or a step that removes rows with blanks, can drop rows without telling you. |
| **2. One number by hand** | Work out one result yourself and compare it with the code's answer. |
| **3. Data types** | A number column stored as text gives wrong math or errors. |
| **4. What got dropped or filled** | Every removed row or filled-in value changes the answer. Count them. |
| **5. Does the statistic fit the shape?** | An AI may use the mean on skewed data. Look at the chart first. |

You've already done most of these checks on your own work:

* **Rows before and after:** you checked `df.shape` in [Look Before You Filter](quest-02-inspect-filter.md). You counted rows after a merge in [One Row Per Group](quest-03-group-columns.md).
* **One number by hand:** in [Looks Right. Is It?](../module-01/quest-10-debugging.md), your total by hand was 286 minutes. That caught a loop that printed 236.
* **Data types:** you named each value's type and kept IDs as text in [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md).
* **Does the statistic fit the shape?:** you picked the median for skewed gifts in [The Loudest Number](quest-01-descriptive-statistics.md).

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
