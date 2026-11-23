# Quest 2.6 — Drop, Fill, or Flag (Missing Data)

**Day 7** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)

## Introduction

Real data almost always has blank cells, and what you do with them changes the answer. For example, a store survey asks customers to rate their visit from 1 to 5, and 30 people skip the question. Count those blanks as 0 and the average rating drops, but delete those customers and you lose all their other answers. This reading covers how to count the gaps, ask why they're missing, and pick one of three moves for each one: drop the row, fill the gap, or flag it. The main takeaway: every gap needs a choice, and every choice needs a reason you can back up with a number.

**Why it matters at work:** What you do with blanks changes every total and average in a report. "I dropped the nulls" isn't a reason, and a teammate, a manager, or an interviewer will ask you why.

## Learning goals

Check off each goal once you can do it.

- [ ] I can count missing values, then ask why they're missing and where.
- [ ] I can choose drop, fill, or flag for each gap, and explain the choice with a number.
- [ ] I can pick a fair stand-in for a fill: the mean, median, mode, forward-fill, or backward-fill.

**Skills:** Data Cleaning & Imputation · Statistical Analysis

## Quick recall

* Recall that you counted the blanks in every column of a new file with `df.isna().sum()`, in [Look Before You Filter](quest-02-inspect-filter.md). `.isna()` marks each empty cell True, and `.sum()` adds them up, because True counts as 1.
* Recall that one very long or very large value pulls the mean up, so the median describes a typical value better on skewed data. You saw this in [The Loudest Number](quest-01-descriptive-statistics.md).

## Words to know

### Missing values

| Word | What it means |
| --- | --- |
| **Missing value** | A cell with no value in it. In a CSV file, it's just an empty field, like `Kai,,,`. |
| **NaN** | How pandas shows an empty cell. It's short for "Not a Number," but it shows up in text columns too. |
| **Placeholder** | A stand-in typed where a real value should be, like `0` or `"unknown"`. It's missing too, but `.isna()` doesn't count it. |

### Why and where is it missing?

Ask these two questions about every gap before you decide anything.

| Word | What it means |
| --- | --- |
| **Never collected** | Nobody asked for the value, like a dog's size when people book by phone. |
| **Lost** | The value existed but didn't get saved, like a walk logged while the app crashed. |
| **Spread out at random** | The gaps are scattered across the data, with no group in common. |
| **Bunched in one group** | The gaps all come from one kind of row, like every phone booking. |

Statistics books give these patterns formal names, such as *missing completely at random* for gaps spread out by chance. You don't need the formal names yet. The two questions are what matter.

### The three choices

| Word | What it means |
| --- | --- |
| **Drop** | Remove a row entirely. It's the right choice when the row has nothing left to work with. |
| **Fill** | Replace a missing value with a stand-in, like the median or the value before it. Filling in missing values is also called **imputation**. |
| **Flag** | Leave the value missing, and add a True/False column that marks it, instead of guessing. |

### Stand-ins for a fill

| Word | What it means | Units |
| --- | --- | --- |
| **Mean** | The average of the real values. One far-off value pulls it toward itself. | Same as the column (for walks, minutes) |
| **Median** | The middle of the real values once they're sorted. One far-off value barely moves it. | Same as the column |
| **Mode** | The value that shows up most often. The usual fill for a category column, when one value clearly repeats the most. | A category, like `"large"` |
| **Forward-fill** | Copy the most recent value before the gap, like yesterday's number. Only makes sense when the rows are in order. | Same as the column |
| **Backward-fill** | Copy the next value after the gap, like tomorrow's number. Helpful when the very first row is blank. | Same as the column |

### Code in this reading

| Code | What it does |
| --- | --- |
| **`.shape`** | Gives a pair of numbers: rows first, then columns. `(8, 4)` means 8 rows and 4 columns. |
| **`.dropna()`** | Removes every row with any blank at all. |
| **`.dropna(subset=["minutes"])`** | Removes only the rows where `minutes` is blank. The parameter `subset` is set to `["minutes"]`, the column that decides the drop. |
| **`.mode()[0]`** | `.mode()` gives back a Series, because a column can have more than one most-common value. `[0]` takes the first one. |
| **`.fillna(value)`** | Puts `value` into every blank in a column, and leaves the real values alone. |
| **`.ffill()`** | Forward-fill: copies the value above into each blank. |
| **`.bfill()`** | Backward-fill: copies the value below into each blank. |

## Before you read

In the reading, you'll focus on Paws & Go, a dog-walking app. Its log has 8 walks. The app crashed during 2 of them, so every field in those rows is blank. People who book by phone are never asked the dog's size, so some rows are missing only the size.

Think about: if you remove every row that has any blank, how many of the 8 walks will you keep? Is that what you want? Write down your first answer, then see if the reading agrees.

## Read

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
| "`dropna()` cleans the data." | With no `subset=`, it throws away every row with any blank, including real records. |
| "Fill with the mean, since it uses every value." | One outlier, like a 95-minute hike, pulls the mean too high. Use the median for skewed data. |
| "The most common category is a safe fill." | Only when it clearly repeats the most. "Large" won with just 2 of 4 known sizes, so filling with it would be a guess. |
| "`.isna()` finds every missing value." | It misses placeholders like `0` or `"unknown"` typed in place of a real value. Look at the rows too. |

### How this connects

* **Next reading:** You'll fix other common problems in a file, like repeated rows and numbers stored as text. Then you'll put all your cleaning steps into one function, so the same decisions run on every new file.
* **Boss Battle (Module Project):** You'll decide whether to drop, fill, or flag the gaps in a real dataset, and write each reason with a number: which rows, why, and how many. Look for placeholder values before you work out any statistics.

## Quick check

**1.** 3 of 40 walks are missing miles because a phone lost GPS. Their minutes are fine. Most walks are 1 to 2 miles, but one hike was 9 miles. What's the best plan?

<details>
<summary>Answer</summary>

Fill the 3 gaps with the median miles, and add a flag column that marks them. The median isn't pulled up by the 9-mile hike, and the flag shows which values were filled in.

</details>

**2.** A teammate writes, "I dropped the nulls." What's missing from that reason?

<details>
<summary>Answer</summary>

Which rows, why they were empty, and how many. For example: "I dropped 2 rows where the app crashed. Both had no minutes, miles, or size, so nothing usable was lost."

</details>

---

**Next:** [Quest 2.7 — Write It Once (Cleaning Functions)](quest-07-cleaning-function.md)
