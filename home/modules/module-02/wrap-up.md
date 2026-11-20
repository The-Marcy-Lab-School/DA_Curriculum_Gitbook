# Module 2 Wrap-Up

{% hint style="success" %}
**You did it.** You took real, messy data from a raw file to a finding someone can act on. That's the core of a data analyst's job.
{% endhint %}

## What you did

* **11 readings**, from descriptive statistics to stakeholder memos
* **5 Data Challenges** on real public data, from college majors to airline safety
* **1 solo lab** on a dataset you'd never seen
* **1 full project**: inspected, cleaned, explored, checked, and explained a real dataset, then presented it

## What you can do now

| Workflow step | You can now... |
| --- | --- |
| **Inspect** | Load any CSV in a notebook and check its shape, data types, blanks, and duplicates |
| **Clean** | Remove repeats by key, fix text that should be numbers, tidy labels, and drop, fill, or flag blanks with a reason, all in a reusable function |
| **Explore** | Pick the mean or the median by looking at the shape, summarize groups, choose a chart that fits, and find a pattern that isn't obvious |
| **Check** | Ask checkable questions about where data came from, and judge an AI's claims against your own numbers |
| **Explain** | Write a README and a memo that stand on their own, and present your finding answer-first |

## How to say it

Employers won't ask "Did you finish Module 2?" They'll ask what you can do. Here's how to describe these skills on a resume and in an interview.

### On your resume

Use your own project's details and numbers:

* **Data Cleaning & Imputation:** "Cleaned a dataset of [your row count] rows in pandas: removed duplicate records by ID, converted text fields to numbers, and documented every missing-value decision."
* **Statistical Analysis and Distributions:** "Profiled key variables with summary statistics and histograms, and reported medians where the data was skewed."
* **Data Mining:** "Found a non-obvious pattern by comparing groups across two columns and ruling out a confound."
* **Data Visualization and Stakeholder Communication:** "Wrote a stakeholder README and data-quality memo with labeled charts and specific, checkable questions about the data."
* **AI Evaluation:** "Checked an AI tool's chart interpretation claim by claim against my own statistics and corrected its errors."

### In an interview

When someone asks about a finding, use this four-part answer from Quest 2.1:

> "I noticed **___**. The numbers show **___**. That means **___**. One caveat is **___**."

For example: "I noticed Downtown's repairs took 15 minutes longer. The numbers show Downtown did mostly screen repairs, and for screen repairs both shops took about 50 minutes. That means the location wasn't the problem. One caveat is that it was only one week of data."

## Where these skills show up next

Nothing you learned here goes away. It comes back in new tools.

| In Module 2, you... | Next, you'll... |
| --- | --- |
| Filtered rows with `df[...]` | Filter rows with `WHERE` in SQL **(Module 3)** |
| Summarized groups with `groupby` | Summarize groups with `GROUP BY` **(Module 3)** |
| Merged tables on a key with `merge` | Combine tables with `JOIN` **(Module 3)** |
| Saw missing values as NaN | See them as `NULL` in a database **(Module 3)** |
| Used pandas on CSV files | Use pandas on data pulled from a database **(Module 4)** |
| Described the shape of your data | Measure how sure you can be about a result **(Module 5)** |
| Made explanatory charts for one stakeholder | Build dashboards in Excel and Tableau for two stakeholders **(Module 6)** |

The habits come with you too: check before you trust, give a reason for every decision, and lead with the answer.

## Before you move on

Can you answer these without looking back?

1. Why can't you trust an average until you know the data's shape?
2. What two things do you check after every merge?
3. What makes a question about data "checkable"?

<details>
<summary>Answers</summary>

1. Outliers and skew pull the mean away from what's typical. Look at the shape, then pick the mean or the median.
2. The row count before and after, and the number of blanks in the new column.
3. It names a specific group, number, or method, so a data steward could answer it with a fact.

</details>

---

**Up next:** Module 3, SQL & Relational Databases. You'll ask the same kinds of questions, this time in a database.
