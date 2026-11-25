# Quest 2.6 — Drop, Fill, or Flag: Missing Data (Day 7)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → **Clean** → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Quick recall

You've found blanks before, one value at a time and then a whole column at once. This reading decides what to do with them.

* `df.isna().sum()` counted the blanks in every column of a new file, in [Look Before You Filter](quest-02-inspect-filter.md). `.isna()` marks each empty cell True, and `.sum()` adds them up, because True counts as 1.
* One very long or very large value pulls the mean up. On skewed data, the median describes a typical value better, as you saw in [The Loudest Number](quest-01-descriptive-statistics.md).
* Your validation function in Module 1's [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md) caught a blank grade, because `"".isdigit()` is `False`. It reported the blank instead of making up a grade.

## Introduction

Real data almost always has blank cells, and what you do with them changes the answer. For example, a store asks 10 customers to rate their visit from 1 to 5. Seven customers answer 5, 4, 4, 5, 3, 4, and 3. Three skip the question.

As in [The Loudest Number](quest-01-descriptive-statistics.md), an average is the sum of the values ÷ the number of values:

* If you skip the blanks: (5 + 4 + 4 + 5 + 3 + 4 + 3) ÷ 7 = 28 ÷ 7 = **4.0**
* If you count the blanks as 0: (28 + 0 + 0 + 0) ÷ 10 = 28 ÷ 10 = **2.8**

The three 0s pull the average down from 4.0 to 2.8, but no customer gave a 0. If you delete those 3 customers instead, you also lose any other answers they gave on the survey. In the picture below, compare the three red 0 cards on the left with the skipped cards on the right.

![Ten rating cards for a store survey, scored 1 to 5. Left, blanks counted as 0: seven grey cards (5, 4, 4, 5, 3, 4, 3) and three red cards that say 0. Average = (5 + 4 + 4 + 5 + 3 + 4 + 3 + 0 + 0 + 0) ÷ 10 = 28 ÷ 10 = 2.8, but no customer gave a 0. Right, blanks skipped: the same seven grey cards and three empty cards marked "skipped." Average = (5 + 4 + 4 + 5 + 3 + 4 + 3) ÷ 7 = 28 ÷ 7 = 4.0, which matches what customers said.](images/blanks-as-zero-ratings.svg)

**Main takeaway:** Every **missing value** needs one of three choices:

* **Drop** the row.
* **Fill** the blank with a stand-in value.
* **Flag** it, and leave it blank.

A missing value is a cell with no value in it, like a skipped survey question. Give each choice a reason with a number, like "I dropped 1 survey where every answer was blank."

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

## Words to know

The examples on this page use the store's survey from the Introduction. It has the same 10 customers and the same 7 ratings. This page adds two more questions:

* `wait_min`: how many minutes the customer waited in line
* `heard_from`: how the customer heard about the store

Here is the survey file. A blank cell means no answer was saved.

| customer | rating | wait_min | heard_from |
| --- | --- | --- | --- |
| C01 | 5 | 4 | *(blank)* |
| C02 | 4 | 30 | *(blank)* |
| C03 | *(blank)* | 5 | *(blank)* |
| C04 | 4 | *(blank)* | friend |
| C05 | 5 | 7 | ad |
| C06 | *(blank)* | 6 | friend |
| C07 | 3 | *(blank)* | web |
| C08 | *(blank)* | *(blank)* | *(blank)* |
| C09 | 4 | 5 | friend |
| C10 | 3 | 6 | ad |

A few facts explain the blanks:

* C01, C02, and C03 filled in an old paper card. It didn't ask how they heard about the store.
* The tablet froze before C04's and C07's wait times were saved.
* C08 tapped Submit without answering anything.
* C02's 30-minute wait is real. The card reader broke while C02 was in line.

### Missing values

| Word | What it means | Example with the survey |
| --- | --- | --- |
| **Missing value** | A cell with no value in it. In a CSV (comma-separated values) file, it's just an empty field (one value's place in a row). | `C08,,,`: C08's rating, wait, and `heard_from` are all empty |
| **NaN** | How pandas shows an empty cell. It's short for "Not a Number," but it shows up in text columns too. | C01 shows `NaN` for `heard_from`, a text column |
| **Placeholder** | A stand-in typed where a real value should be, like `0` or `"unknown"`. It's missing too, but `.isna()` doesn't count it. | If the 3 skipped ratings were typed as `0`, `.isna()` would count **0** blanks in `rating` |

A placeholder `0` is a quiet problem, like the bare `except:` in [Looks Right. Is It?](../module-01/quest-10-debugging.md) that returned 0. Both hide a problem behind a 0 that looks real.

### Why and where is it missing?

Ask these two questions about every gap before you decide anything.

| Word | What it means | Example with the survey |
| --- | --- | --- |
| **Never collected** | Nobody asked for the value. | `heard_from` for C01, C02, and C03: the old paper card didn't ask |
| **Lost** | The value existed but didn't get saved. | C04's and C07's wait times, typed while the tablet froze |
| **Spread out at random** | The gaps are scattered across the data, with no group in common. | The 3 skipped ratings, from C03, C06, and C08, with nothing in common |
| **Bunched in one group** | The gaps all come from one kind of row. | The 3 blank `heard_from` cells left after the drop all come from old paper cards |

### The three choices

| Word | What it means | Example with the survey |
| --- | --- | --- |
| **Drop** | Remove a row entirely. It's the right choice when the row has nothing left to work with. | Drop C08's row, where every answer is blank: 10 rows become **9** |
| **Fill** | Replace a missing value with a stand-in, like the median or the value before it. Filling in missing values is also called **imputation**. | Fill C04's and C07's wait times with the median, **6.0 minutes** |
| **Flag** | Leave the value missing, and add a True/False column that marks it, instead of guessing. | After the drop, `heard_unknown` is True for **3** customers |

A flag works like the list of problems your validation function returned. It records which rows had a gap, so you can count them and report them, without guessing a value.

### Stand-ins for a fill

**Units** are what a number counts or measures. A fill comes out in the same units as the column: here, minutes. The mode is the exception: it's a category, like `"friend"`. Most examples use the wait times after C08's row is dropped. The rows are in the order customers came in:

`4, 30, 5, blank, 7, 6, blank, 5, 6` (in minutes, from C01 to C10, without C08)

| Word | What it means | Example with the survey |
| --- | --- | --- |
| **Mean** | The average of the real values. One far-off value pulls it toward itself. | (4 + 30 + 5 + 7 + 6 + 5 + 6) ÷ 7 = 63 ÷ 7 = **9.0 minutes** |
| **Median** | The middle of the real values once they're sorted. One far-off value barely moves it. | Sorted: 4, 5, 5, 6, 6, 7, 30. The 4th of 7 = **6.0 minutes** |
| **Mode** | The value that shows up most often. The usual fill for a category column, when one value clearly repeats the most. | Known `heard_from` answers: friend, ad, friend, web, friend, ad. **"friend"**, but with only 3 of 6 |
| **Forward-fill** | Copy the most recent value before the gap, like the customer just before in line. Only makes sense when the rows are in order. | C04 gets C03's **5**. C07 gets C06's **6**. |
| **Backward-fill** | Copy the next value after the gap, like the customer just after in line. Helpful when the very first row is blank. | C04 gets C05's **7**. C07 gets C09's **5**. |

### Code in this reading

| Code | What it does |
| --- | --- |
| **`.shape`** | Gives a pair of numbers: rows first, then columns. On the survey, `(10, 4)` means 10 rows and 4 columns. |
| **`.dropna()`** | Removes every row with any blank at all. On the survey, 10 rows become **3**. |
| **`.dropna(subset=["rating"])`** | Removes only the rows where `rating` is blank. The parameter `subset` is set to `["rating"]`, the column that decides the drop. On the survey, 10 rows become **7**. |
| **`.mode()[0]`** | `.mode()` gives back a Series, because a column can have more than one most-common value. `[0]` takes the first one. For the known `heard_from` answers, it gives `"friend"`. |
| **`.fillna(value)`** | Puts `value` into every blank in a column, and leaves the real values alone. With the median, C04's and C07's wait times both become **6.0**. |
| **`.ffill()`** | Forward-fill: copies the value above into each blank. C04 gets **5**, and C07 gets **6**. |
| **`.bfill()`** | Backward-fill: copies the value below into each blank. C04 gets **7**, and C07 gets **5**. |

## Before you read

In the reading, you'll focus on Paws & Go, a dog-walking app. Its log has 8 walks. The app crashed during 2 of them, so every field in those rows is blank. People who book by phone are never asked the dog's size, so some rows are missing only the size.

Think about: if you remove every row that has any blank, how many of the 8 walks will you keep? Is that what you want? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

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

The picture below shows the two questions that decide between drop, fill, and flag. Its drop example is C08's blank survey.

![A decision flow titled "Drop, fill, or flag: two questions decide." A value is missing. First question: is anything useful left in the row? If no, drop the row, for example when a customer skipped every question. If yes, ask: is there a fair stand-in, like the median, the mode, or the value before? If yes, fill it, say what you used, and add a column that marks the filled rows. If no, flag it: keep the blank and add a True/False column that marks it.](images/drop-fill-flag.svg)

| Fill with | Fits best when |
| --- | --- |
| Mean | The values are roughly balanced, with no outliers |
| Median | The data is skewed or has real outliers, like C02's 30-minute wait |
| Mode | The column holds categories, and one value clearly repeats the most |
| Forward-fill (`.ffill()`) | The rows are in order, and each value is close to the one before it |
| Backward-fill (`.bfill()`) | The rows are in order, and the first row (or a stretch at the start) is blank |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I'll run `dropna()` to clean the data." | With no `subset=`, it keeps only 3 of the 10 customers. It throws away C01's and C02's real ratings just because `heard_from` is blank. |
| "The mean uses every wait time, so it's the fairest fill." | C02's 30-minute wait pulls the mean up to 9.0 minutes, longer than 6 of the 7 real waits. The median, 6.0, sits among them. |
| "Friend is the most common answer, so I'll fill the blanks with it." | "Friend" won with just 3 of 6 known answers. All 3 blanks come from old paper cards, so filling with it would be a guess. |
| "`.isna().sum()` shows 0 for this column, so nothing is missing." | It misses placeholders like `0` or `"unknown"` typed in place of a real value. If the 3 skipped ratings were typed as 0, it would show 0, and the average would drop to 2.8. Look at the rows too. |

### How this connects

* **Next reading:** You'll fix other common problems in a file, like repeated rows and numbers stored as text. Then you'll put all your cleaning steps into one function, so the same decisions run on every new file.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll decide whether to drop, fill, or flag the gaps in a real dataset, and write each reason with a number: which rows, why, and how many. Look for placeholder values before you work out any statistics.

## Quick check

**1.** A month later, 3 of 40 surveys are missing the wait time because the tablet froze. Their ratings are fine. Most waits are 3 to 8 minutes, but one was 30 minutes. What's the best plan?

<details>
<summary>Answer</summary>

Fill the 3 gaps with the median wait, and add a flag column that marks them. The median isn't pulled up by the 30-minute wait, and the flag shows which values were filled in.

</details>

**2.** A teammate writes, "I dropped the nulls." (A **null** is another name for a missing value.) What's missing from that reason?

<details>
<summary>Answer</summary>

Which rows, why they were empty, and how many. For example: "I dropped 1 row, C08's survey. It had no rating, wait time, or `heard_from`, so nothing usable was lost."

</details>

---

**Next:** [Quest 2.7 — Write It Once: Cleaning Functions (Day 8)](quest-07-cleaning-function.md)
