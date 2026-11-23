# Quest 2.3 — One Row Per Group (Grouping, New Columns, and Merging)

**Day 3** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)

## Introduction

Managers rarely ask about one row. For example, a pizza chain logs every order: which store, what time, and how much it cost. The owner asks, "Which store sells the most?" You can't read 5,000 orders by eye, and writing a separate filter for every store gets old fast. This reading covers how to turn many rows into one summary row per group, add new columns worked out from the ones you have, change rows safely, and bring in columns from a second table. The main takeaway: compare groups with one summary row per group, and check your work after every change, because pandas can quietly do nothing or leave blanks without an error.

**Why it matters at work:** Questions like "Which location collects the most?" or "Which team is slowest?" are answered by comparing groups. Most findings start this way.

## Learning goals

Check off each goal once you can do it.

- [ ] I can summarize a column for each group, and keep the count next to the mean and median.
- [ ] I can add a new column calculated from other columns, and change rows in the original table safely.
- [ ] I can merge in columns from a lookup table and check that the merge worked.

**Skills:** Data Mining · pandas DataFrames

## Quick recall

* Recall that you kept only the rows that matched two conditions, each in its own parentheses, joined with `&`, in [Look Before You Filter](quest-02-inspect-filter.md): `df[(df["site"] == "Eastside") & (df["category"] == "Produce")]`.
* Recall that `df.isna().sum()` counted the blank cells in each column, in the same reading. You'll use that count again to check your work.
* Recall that when the mean and median are close, no single far-off value is pulling the mean, from [The Loudest Number](quest-01-descriptive-statistics.md).

## Words to know

### Grouping

| Word | What it means | Units |
| --- | --- | --- |
| **groupby** | Splits rows into groups by a category, applies a summary to each group, and combines the answers into one row per group. People call this "split, apply, combine." On its own, `groupby("site")` only makes the groups. It shows no table until you add a summary. | — |
| **Aggregation** | A summary worked out for each group, such as a count, mean, or median. `.agg()` does several at once. | Depends on the summary (see below) |
| **count** (in `.agg()`) | How many values in the group are *not* blank. It shows how many rows each number rests on, so you can spot a group too small to trust. | A count of rows |
| **mean and median** (in `.agg()`) | The average and the middle value for each group. Side by side, they're a quick skew check for each group. | Same as the column (here, units of blood) |

### New columns

| Word | What it means |
| --- | --- |
| **Derived column** | A new column worked out from columns you already have. You write the formula once, and pandas applies it to every row at once, with no loop. A blank in, a blank (NaN) out. |
| **Rate** | A derived column that divides one number by another, like units per volunteer hour. It can show what raw counts hide. Its units come from both columns: units of blood *per hour*. |
| **Mask** | A True/False column saved under a name, like `big = drives["units"] >= 30`, so you can reuse it to pick rows. |

### Changing rows safely

| Word | What it means |
| --- | --- |
| **Copy** | A separate table. In pandas 3, a filter like `drives[big]` always gives you a copy. Changing a copy never touches the original. |
| **Chained assignment** | Setting a value in two steps, like `df[mask]["col"] = value`. The first step makes a copy, and the second step changes the copy, so your table stays the same. |
| **ChainedAssignmentError** | The message pandas shows when you try chained assignment. Despite its name, it's a warning, not a crash: the cell keeps running, so it's easy to miss. |
| **`.loc`** | Names the rows and the column inside one pair of brackets, so the change happens to your table itself, in one step: `df.loc[rows, "col"] = value`. |

### Combining tables

| Word | What it means |
| --- | --- |
| **Merge** | Combines two tables by matching rows on a shared column, then copies the second table's columns onto the matching rows. |
| **Key** | The shared column a merge matches on, like `site`. Keys must match exactly, letter for letter. |
| **Lookup table** | A small second table with one row per key, used to add columns to a bigger table. |
| **Left merge** (`how="left"`) | Setting the parameter `how` to `"left"` makes a merge keep every row of your main table. A row with no match stays, with NaN in the new columns. |

## Before you read

In the reading, you'll focus on a nonprofit that runs blood drives at a library, a community center, and a fire station. A volunteer writes one row per drive. A unit is one bag of donated blood. The team asks, "Which place collects the most blood?"

Think about: besides each place's average, what else would you want to know before you call one place the winner? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Why the count for one site comes out lower than the number of drives it held.
2. Why changing filtered rows in two steps leaves the original table unchanged.
3. What the two checks after a merge catch that an error message doesn't.

**[Start the reading: One Row Per Group →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/pandas-group-columns/reading-1-one-row-per-group/)** (about 20 minutes)

## Main takeaways

### Summary

* **`groupby` splits, applies, and combines.** Keep the count next to the mean and median, so you can spot a group too small to trust. `count` skips blanks.
* **A filter gives you a copy.** To change rows in the original table, use `df.loc[rows, "column"] = value` in one step. Then check the count, because a step that silently does nothing is worse than a crash.
* **After every merge, check two things:** the row count before and after, and the number of blanks in the new column. Keys must match letter for letter.

![Eight blood-drive rows are split into one pile per site. The mean units of each pile is worked out, skipping the one blank value: Community Center 38.0, Fire Station 22.0, Library 27.3. Then the answers are combined into a table with one row per site. The line of code is drives.groupby("site")["units"].mean().](images/groupby-split-apply-combine.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`groupby("site")` on its own shows a table." | It only makes the groups. You still need a summary like `.mean()` or `.agg()`. |
| "Adding `.copy()` makes a two-step change stick." | It still changes a copy. Use `.loc` in one step. |
| "ChainedAssignmentError stopped my cell, so nothing happened." | It's a warning. The cell keeps running, and every count after it is quietly wrong. |
| "The merge ran with no error, so it worked." | A misspelled key leaves blanks silently. Count the blanks to find out. |

### How this connects

* **Next reading:** You'll turn group summaries like these into charts: quick, rough ones to find a pattern for yourself, and one clear chart for someone who wasn't there while you explored.
* **Boss Battle (Module Project):** When you look for a finding in a real dataset, you'll compare groups with one summary row per group, add new columns when raw numbers hide something, and check your row counts and blanks after every change.

## Quick check

**1.** What does `drives.groupby("site")["units"].agg(["count", "mean"])` give you?

<details>
<summary>Answer</summary>

One row per site, showing how many drives had a units value (count) and the average units (mean) for that site.

</details>

**2.** Your lookup table spells a site "Firehouse," but your main table says "Fire Station." What happens after a left merge?

<details>
<summary>Answer</summary>

The merge runs with no error. Every Fire Station row stays in the table, but with a blank in the new column. Counting blanks after the merge is how you'd catch it.

</details>

---

**Next:** [Quest 2.4 — Who's This Chart For? (Exploratory vs. Explanatory Charts)](quest-04-two-kinds-of-charts.md)
