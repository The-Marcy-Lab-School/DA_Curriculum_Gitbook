# Quest 2.6 — Drop, Fill, or Flag: Missing Data (Day 7)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → **Clean** → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Real data almost always has blank cells, and what you do with them changes the answer. For example, a store asks 10 customers to rate their visit from 1 to 5. Seven customers answer 5, 4, 4, 5, 3, 4, and 3. Three skip the question.

Recall that an average is the sum of the values ÷ the number of values:

* If you skip the blanks: (5 + 4 + 4 + 5 + 3 + 4 + 3) ÷ 7 = 28 ÷ 7 = **4.0**
* If you count the blanks as 0: (28 + 0 + 0 + 0) ÷ 10 = 28 ÷ 10 = **2.8**

The three 0s pull the average down from 4.0 to 2.8, but no customer gave a 0. If you delete those 3 customers instead, you lose all their other answers on the survey.

![Ten rating cards for a store survey, scored 1 to 5. Left, blanks counted as 0: seven grey cards (5, 4, 4, 5, 3, 4, 3) and three red cards that say 0. Average = (5 + 4 + 4 + 5 + 3 + 4 + 3 + 0 + 0 + 0) ÷ 10 = 28 ÷ 10 = 2.8, but no customer gave a 0. Right, blanks skipped: the same seven grey cards and three empty cards marked "skipped." Average = (5 + 4 + 4 + 5 + 3 + 4 + 3) ÷ 7 = 28 ÷ 7 = 4.0, which matches what customers said.](images/blanks-as-zero-ratings.svg)

**Main takeaway:** Every **missing value** needs one of three choices:

* **Drop** the row.
* **Fill** the blank with a stand-in value.
* **Flag** it, and leave it blank.

A missing value is a cell with no value in it, like a skipped survey question. Give each choice a reason with a number, like "I dropped 2 rows where the app crashed."

**Why it matters at work:** What you do with blanks decides the totals and averages in a report. For example, analysts handle blanks before they:

* report a store's average customer rating
* add up how many hours each worker worked this week
* compare sales by month when some days weren't recorded

If you count 3 skipped ratings as 0, the average drops from 4.0 to 2.8. The store looks worse than it is. A teammate, a manager, or an interviewer will also ask why you chose drop, fill, or flag.

## Learning goals

After this reading, you should be able to say:

* I can count missing values, then ask why they're missing and where.
* I can choose drop, fill, or flag for each gap, and explain the choice with a number.
* I can pick a fair stand-in for a fill: the mean, median, mode, forward-fill, or backward-fill.

**Skills:** Data Cleaning & Imputation · Statistical Analysis

## Quick recall

You've found blanks before, one value at a time and then a whole column at once. This reading decides what to do with them.

* Recall that you counted the blanks in every column of a new file with `df.isna().sum()`, in [Look Before You Filter](quest-02-inspect-filter.md). `.isna()` marks each empty cell True, and `.sum()` adds them up, because True counts as 1.
* Recall that one very long or very large value pulls the mean up, so the median describes a typical value better on skewed data. You saw this in [The Loudest Number](quest-01-descriptive-statistics.md).
* Recall that `"".isdigit()` is `False`, so your validation function caught a blank grade, in [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md). It reported the blank. It didn't make up a grade.

## Words to know

### Missing values

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Missing value** | A cell with no value in it. In a CSV (comma-separated values) file, it's just an empty field (one value's place in a row). | `Kai,,,`: Kai's minutes, miles, and size are all empty |
| **NaN** | How pandas shows an empty cell. It's short for "Not a Number," but it shows up in text columns too. | Ana's first walk shows `NaN` for `dog_size`, a text column |
| **Placeholder** | A stand-in typed where a real value should be, like `0` or `"unknown"`. It's missing too, but `.isna()` doesn't count it. | If a size were typed as `"unknown"`, `.isna()` would not count it |

A placeholder `0` is a quiet problem, like the bare `except:` in [Looks Right. Is It?](../module-01/quest-10-debugging.md) that returned 0. Both hide a problem behind a 0 that looks real.

### Why and where is it missing?

Ask these two questions about every gap before you decide anything.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Never collected** | Nobody asked for the value. | A dog's size when people book (schedule a walk) by phone |
| **Lost** | The value existed but didn't get saved. | Kai's and Lee's walks, logged (recorded) while the app crashed |
| **Spread out at random** | The gaps are scattered across the data, with no group in common. | One blank on Sam's walk, one on Ana's, one on Kai's, with nothing in common |
| **Bunched in one group** | The gaps all come from one kind of row. | The 2 blank sizes left after the drop are both phone bookings |

Statistics books give these patterns formal names, such as *missing completely at random* for gaps spread out by chance. You don't need the formal names yet. The two questions are what matter.

### The three choices

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Drop** | Remove a row entirely. It's the right choice when the row has nothing left to work with. | Drop Kai's and Lee's crashed rows: 8 walks become **6** |
| **Fill** | Replace a missing value with a stand-in, like the median or the value before it. Filling in missing values is also called **imputation**. | Fill Lee's day 3 and day 7 with the median, **43.0 minutes** |
| **Flag** | Leave the value missing, and add a True/False column that marks it, instead of guessing. | `size_unknown` is True for **2** walks |

A flag works like the list of problems your validation function returned. It records which rows had a gap, so you can count them and report them, without guessing a value.

### Stand-ins for a fill

**Units** are what a number counts or measures. A fill comes out in the same units as the column: here, minutes. The mode is the exception: it's a category, like `"large"`. Most examples use Lee's 8 days of walks, in minutes:

`40, 45, blank, 42, 95, 44, blank, 41` (day 5 was a 95-minute hike)

| Word | What it means | Example with Lee's walks |
| --- | --- | --- |
| **Mean** | The average of the real values. One far-off value pulls it toward itself. | (40 + 45 + 42 + 95 + 44 + 41) ÷ 6 = 307 ÷ 6 = **51.2 minutes** |
| **Median** | The middle of the real values once they're sorted. One far-off value barely moves it. | Sorted: 40, 41, 42, 44, 45, 95. (42 + 44) ÷ 2 = **43.0 minutes** |
| **Mode** | The value that shows up most often. The usual fill for a category column, when one value clearly repeats the most. | Known sizes: small, large, medium, large. **"large"**, but with only 2 of 4 |
| **Forward-fill** | Copy the most recent value before the gap, like yesterday's number. Only makes sense when the rows are in order. | Day 3 gets day 2's **45**. Day 7 gets day 6's **44**. |
| **Backward-fill** | Copy the next value after the gap, like tomorrow's number. Helpful when the very first row is blank. | Day 3 gets day 4's **42**. Day 7 gets day 8's **41**. |

### Code in this reading

| Code | What it does |
| --- | --- |
| **`.shape`** | Gives a pair of numbers: rows first, then columns. `(8, 4)` means 8 rows and 4 columns. |
| **`.dropna()`** | Removes every row with any blank at all. On the walk log, 8 rows become **4**. |
| **`.dropna(subset=["minutes"])`** | Removes only the rows where `minutes` is blank. The parameter `subset` is set to `["minutes"]`, the column that decides the drop. On the walk log, 8 rows become **6**. |
| **`.mode()[0]`** | `.mode()` gives back a Series, because a column can have more than one most-common value. `[0]` takes the first one. For the known sizes, it gives `"large"`. |
| **`.fillna(value)`** | Puts `value` into every blank in a column, and leaves the real values alone. With the median, Lee's day 3 and day 7 both become **43.0**. |
| **`.ffill()`** | Forward-fill: copies the value above into each blank. Lee's day 3 gets **45**, and day 7 gets **44**. |
| **`.bfill()`** | Backward-fill: copies the value below into each blank. Lee's day 3 gets **42**, and day 7 gets **41**. |

## Before you read

In the reading, you'll focus on Paws & Go, a dog-walking app. Its log has 8 walks. The app crashed during 2 of them, so every field in those rows is blank. People who book by phone are never asked the dog's size, so some rows are missing only the size.

Think about: if you remove every row that has any blank, how many of the 8 walks will you keep? Is that what you want? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. The two questions to ask about every gap before you decide anything.
2. Why filling with the mode would just be a guess for the dog sizes.
3. Which fill puts a number into Lee's missing days that's longer than almost every real walk.

**[Start the reading: Drop, Fill, or Flag →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/missing-data/reading-1-dropfillorflag/)** (about 20 minutes)

## Main takeaways

### Summary

* **Count the gaps first** with `.isna().sum()`. Then ask *why* each one is missing (never collected, or lost?) and *where* (spread out, or bunched in one group?).
* **Drop a row only when nothing useful is left,** and use `subset=` so rows with real values survive.
* **Fill when a fair stand-in exists, and flag when a fill would be a guess.** You can do both: save a flag column first, then fill, so readers know which values were filled in. Always say which rows, why, and how many.

![A decision flow titled "Drop, fill, or flag: two questions decide." A value is missing. First question: is anything useful left in the row? If no, drop the row, for example when the app crashed and every field is blank. If yes, ask: is there a fair stand-in, like the median, the mode, or the value before? If yes, fill it, say what you used, and add a column that marks the filled rows. If no, flag it: keep the blank and add a True/False column that marks it.](images/drop-fill-flag.svg)

| Fill with | Fits best when |
| --- | --- |
| Mean | The values are roughly balanced, with no outliers |
| Median | The data is skewed or has real outliers, like Lee's 95-minute hike |
| Mode | The column holds categories, and one value clearly repeats the most |
| Forward-fill (`.ffill()`) | The rows are in order, and each value is close to the one before it |
| Backward-fill (`.bfill()`) | The rows are in order, and the first row (or a stretch at the start) is blank |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I'll run `dropna()` to clean the data." | With no `subset=`, it keeps only 4 of the 8 walks. It throws away Ana's and Kai's real walks just because the size is blank. |
| "The mean uses every walk, so it's the fairest fill." | Lee's 95-minute hike pulls the mean up to 51.2 minutes, longer than 5 of Lee's 6 real walks. The median, 43.0, sits among them. |
| "Large is the most common size, so I'll fill the blanks with it." | "Large" won with just 2 of 4 known sizes, so filling with it would be a guess. |
| "`.isna().sum()` shows 0 for this column, so nothing is missing." | It misses placeholders like `0` or `"unknown"` typed in place of a real value. Look at the rows too. |

### How this connects

* **Next reading:** You'll fix other common problems in a file, like repeated rows and numbers stored as text. Then you'll put all your cleaning steps into one function, so the same decisions run on every new file.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll decide whether to drop, fill, or flag the gaps in a real dataset, and write each reason with a number: which rows, why, and how many. Look for placeholder values before you work out any statistics.

## Quick check

**1.** 3 of 40 walks are missing miles because a phone lost GPS (Global Positioning System, the signal that tracks location). Their minutes are fine. Most walks are 1 to 2 miles, but one hike was 9 miles. What's the best plan?

<details>
<summary>Answer</summary>

Fill the 3 gaps with the median miles, and add a flag column that marks them. The median isn't pulled up by the 9-mile hike, and the flag shows which values were filled in.

</details>

**2.** A teammate writes, "I dropped the nulls." (A **null** is another name for a missing value.) What's missing from that reason?

<details>
<summary>Answer</summary>

Which rows, why they were empty, and how many. For example: "I dropped 2 rows where the app crashed. Both had no minutes, miles, or size, so nothing usable was lost."

</details>

---

**Next:** [Quest 2.7 — Write It Once: Cleaning Functions (Day 8)](quest-07-cleaning-function.md)
