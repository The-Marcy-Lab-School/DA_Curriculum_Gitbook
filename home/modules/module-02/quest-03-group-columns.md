# Quest 2.3 — One Row Per Group: Grouping, New Columns, and Merging (Day 3)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Managers rarely ask about just one row. For example, a pizza company has 20 stores. It records every order: the store, the time, and the price. The owner asks, "Which store sells the most?" There are 5,000 orders, too many to read one by one. You could write one filter per store, but that's 20 filters. One line of code can make one summary row for each store instead.

**Main takeaway:** To compare groups, **group** the rows. Split them into one pile per group. Then work out one summary number for each pile. In pandas, `groupby` does this in one line. Check your work after every change, because pandas can sometimes do nothing, or add blanks, without showing an error.

**Why it matters at work:** Comparing groups is how analysts answer most "which one?" questions. For example, teams use one summary row per group to:

* find which store sells the most
* see which support team takes the longest to answer customer calls
* compare average sales for each month

Without the count for each group, you might call a store the winner when it had only 2 orders.

## Learning goals

After this reading, you should be able to say:

* I can summarize a column for each group, and keep the count next to the mean and median.
* I can add a new column calculated from other columns, and change rows in the original table safely.
* I can merge in columns from a lookup table and check that the merge worked.

**Skills:** Data Mining · Statistical Analysis

## Quick recall

You've added up values in a loop, and looked up values by key. This reading does both for a whole table at once.

* In [Look Before You Filter](quest-02-inspect-filter.md), you kept only the rows that matched two conditions, each in its own parentheses, joined with `&`: `df[(df["site"] == "Eastside") & (df["category"] == "Produce")]`.
* `df.isna().sum()` counted the blank cells in each column, also in [Look Before You Filter](quest-02-inspect-filter.md). You'll use that count again to check your work after a merge.
* In Module 1's [Lookups Matter](../module-01/quest-09-big-o-practice.md), you built a dictionary once, then found values by key with `.get()`, which gave `None` for a missing key. A merge looks up keys the same way, but a missing key gives NaN.

## Words to know

### Grouping

**Units** are what a number counts or measures. In this reading, the `units` column counts bags of blood: one unit is one bag. So each site's mean and median come out in units of blood. A count comes out in drives. The examples use the `units` column of the reading's `drives.csv`:

* Library: 26, 31, 25
* Community Center: 40, blank, 36
* Fire Station: 20, 24

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **groupby** | Splits rows into groups by a category, applies a summary to each group, and combines the answers into one row per group. People call this "split, apply, combine." On its own, `groupby("site")` only makes the groups. It shows no table until you add a summary. | `drives.groupby("site")` makes **3 groups**, one per site |
| **Aggregation** | A summary worked out for each group, such as a count, mean, or median. `.agg()` does several at once. | `.agg(["count", "mean", "median"])` gives **3 numbers** for each site |
| **count** (in `.agg()`) | How many values in the group are *not* blank. It shows how many rows each number rests on, so you can spot a group too small to trust. | Community Center held 3 drives, but 1 is blank, so its count is **2 drives** |
| **mean and median** (in `.agg()`) | The average and the middle value for each group. Side by side, they're a quick skew check for each group. | Library mean: (26 + 31 + 25) ÷ 3 = 82 ÷ 3 = **27.3 units**. Median: **26 units**. |

You've built a summary like this by hand. In [One Job at a Time](../module-01/quest-07-second-function.md), `summarize_steps` looped over each day and kept a running total with `total += steps`. To total each site that way, you'd need a separate total for every site. `groupby` keeps one for every group, with no loop.

### New columns

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Derived column** | A new column worked out from columns you already have. You write the formula once, and pandas applies it to every row at once, with no loop. A blank in, a blank (NaN) out. | `units_per_hour`: the first Library drive is 26 units ÷ 10 hours = **2.6**. The blank drive gives **NaN**. |
| **Rate** | A derived column that divides one number by another, like units per volunteer hour. It can show what raw counts hide. Its units come from both columns: units of blood *per hour*. | Fire Station collects the fewest units. But per hour, its drives (20 ÷ 8 = **2.5**, 24 ÷ 8 = **3.0**) are close to the Library's (**2.6** to **3.1**). |
| **Mask** | A True/False column saved under a name, like `big = drives["units"] >= 30`, so you can reuse it to pick rows. | `big` is True for **3 drives**: 40, 31, and 36 units |

In [Trace the Path](../module-01/quest-01-control-flow.md), `for temp in temps:` checked `temp > 80` on one number per pass. A derived column or a mask does the same kind of math or check on every row at once.

### Changing rows safely

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Copy** | A separate table. In pandas 3, a filter like `drives[big]` always gives you a copy. Changing a copy never touches the original. | `drives[big]` is a 3-row copy |
| **Chained assignment** | Setting a value in two steps, like `df[mask]["col"] = value`. The first step makes a copy, and the second step changes the copy, so your table stays the same. | After `drives[big]["goal_met"] = "yes"`, `drives` has **0** "yes" values |
| **ChainedAssignmentError** | The message pandas shows when you try chained assignment. Despite its name, it's a warning, not a crash: the cell keeps running, so it's easy to miss. | It shows under that same line, and the next line still runs |
| **`.loc`** | Names the rows and the column inside one pair of brackets, so the change happens to your table itself, in one step: `df.loc[rows, "col"] = value`. | After `drives.loc[big, "goal_met"] = "yes"`, `drives` has **3** "yes" values |

### Combining tables

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Merge** | Combines two tables by matching rows on a shared column, then copies the second table's columns onto the matching rows. | Each drive gets its site's `neighborhood`, like Library → Northside |
| **Key** | The shared column a merge matches on, like `site`. Keys must match exactly, letter for letter. | `"Firehouse"` does not match `"Fire Station"` |
| **Lookup table** | A small second table with one row per key, used to add columns to a bigger table. | 3 rows: one per site, with its neighborhood |
| **Left merge** (`how="left"`) | Setting the parameter `how` to `"left"` makes a merge keep every row of your main table. A row with no match stays, with NaN in the new columns. | 8 rows before, **8** after. With `"Firehouse"`, **2** neighborhoods are blank. |

## Before you read

In the reading, you'll focus on a nonprofit that runs blood drives at a library, a community center, and a fire station. A **nonprofit** is a group that works for a cause, not to make money. A **blood drive** is an event where people come to give blood. A volunteer writes one row per drive. A unit is one bag of donated blood. The team asks, "Which place collects the most blood?"

Think about: besides each place's average, what else would you want to know before you call one place the winner? Write down your first answer, then see if the reading agrees.

## ⭐ Read

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

The picture below shows `groupby` on the drives: split the rows by site, find each site's mean, then combine.

![Eight blood-drive rows are split into one pile per site. The mean units of each pile is worked out, skipping the one blank value: Community Center 38.0, Fire Station 22.0, Library 27.3. Then the answers are combined into a table with one row per site. The line of code is drives.groupby("site")["units"].mean().](images/groupby-split-apply-combine.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I ran `drives.groupby("site")`, so I should see one row per site." | It only makes the groups. You still need a summary like `.mean()` or `.agg()`. |
| "If I add `.copy()`, my two-step change will work." | It still changes a copy, so `drives` still has 0 "yes" values. Use `.loc` in one step to get all 3. |
| "ChainedAssignmentError stopped my cell, so nothing happened." | It's a warning. The cell keeps running, and every count after it is quietly wrong. |
| "The merge ran with no error, so it worked." | With `"Firehouse"` in the lookup, the merge runs with no error, but 2 rows get a blank neighborhood. Count the blanks to find out. |

### How this connects

* **Next reading:** You'll turn group summaries like these into charts: quick, rough ones to find a pattern for yourself, and one clear chart for someone who wasn't there while you explored.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** When you look for a finding in a real dataset, you'll compare groups with one summary row per group, add new columns when raw numbers hide something, and check your row counts and blanks after every change.

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

**Next:** [Quest 2.4 — Who's This Chart For? Exploratory vs. Explanatory Charts (Day 4)](quest-04-two-kinds-of-charts.md)
