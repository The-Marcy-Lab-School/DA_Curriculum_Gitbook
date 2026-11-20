# Tool Guide: pandas

{% hint style="info" %}
**In one sentence:** pandas is a free Python library for working with tables of data, like a spreadsheet you control with code.
{% endhint %}

## Why analysts use it

pandas is one of the most used tools in data jobs. It can load a file with thousands of rows in one line, check it for problems, clean it, and summarize it by group. Because every step is written as code, you can run the same steps again on next month's file, and someone else can check exactly what you did.

## The main idea: the DataFrame

A **DataFrame** is pandas' table. It has rows and named columns, and each column has its own data type (its **dtype**), such as text (`str`) or decimal numbers (`float64`).

```text
   site      category  weight_lbs     <- column names
0  Eastside  Produce   12.0           <- each row is one record
1  Downtown  Canned    40.0
```

## What you'll learn about it in Module 2

| Where | What you'll do |
| --- | --- |
| Quest 2.2 (Day 2) | Load a CSV, check it four ways, filter rows, sort |
| Quest 2.3 (Day 3) | Summarize by group, add new columns, change rows safely, merge two tables |
| Quest 2.4 (Day 4) | Turn text into real dates and count rows per day |
| Quest 2.6 (Day 7) | Drop, fill, or flag missing values |
| Quest 2.7 (Day 8) | Remove repeated rows, turn text into numbers, tidy labels, and wrap it all in a function |
| Quest 2.8 (Day 9) | Group by two columns at once to find a real pattern |

## The lines you'll use most

```python
import pandas as pd                  # load pandas and call it pd

df = pd.read_csv("data.csv")         # read a file into a DataFrame
df.shape                             # (rows, columns)
df.dtypes                            # each column's data type
df.isna().sum()                      # blanks in each column
df.duplicated().sum()                # rows that repeat an earlier row
df[df["site"] == "Eastside"]         # keep only matching rows
df.groupby("site")["units"].mean()   # one summary per group
```

## Common first-day problems

| Problem | Fix |
| --- | --- |
| A number column shows `str` | Something in it isn't a clean number, like `"12 lbs"` or `"TBD"`. You'll fix this on Day 8. |
| A filter with two conditions gives a `TypeError` | Put each condition in its own parentheses and join them with `&`: `df[(a) & (b)]` |
| A tutorial or AI answer says `object` for text | That's the old name for text columns. pandas 3 shows `str`. |
| A change to filtered rows didn't stick | A filter gives you a copy. Change the original with `df.loc[rows, "column"] = value`. |

## Getting started resources

* [pandas: Getting started tutorials](https://pandas.pydata.org/docs/getting_started/intro_tutorials/index.html) (official, short, with pictures)
* [10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html) (official quick tour)
* [Kaggle Learn: Pandas](https://www.kaggle.com/learn/pandas) (free, hands-on practice in your browser)

---

**Next:** [Quest 2.2 — Look Before You Filter](quest-02-inspect-filter.md)
