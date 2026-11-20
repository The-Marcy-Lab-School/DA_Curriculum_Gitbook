# Quest 2.2 — Look Before You Filter (Day 2)

{% hint style="info" %}
**In one sentence:** Before you answer any question with a new file, check it four ways, because one blank or one repeated row can make every total wrong.
{% endhint %}

## Why this matters

Almost every data task starts the same way: load a file, check it, then pull out the rows you need. A manager asking "How much produce came in?" can get an answer from one line of code. If the file has a blank weight or a donation logged twice, that answer is wrong, and nobody will know unless you checked.

## What you'll be able to do

* I can load a CSV file into a notebook and explain what the kernel remembers.
* I can run four checks on any new file: shape, data types, missing values, and duplicates.
* I can filter rows on one or two conditions and sort the result.

**Skills:** pandas DataFrames · Data Cleaning & Imputation
**New tools today:** Jupyter notebooks and pandas. Read the [Notebooks guide](tool-jupyter-notebooks.md) and the [pandas guide](tool-pandas.md) first (10 minutes).

## Words to know

| Word | What it means |
| --- | --- |
| **DataFrame** | pandas' table. It has rows and named columns. |
| **dtype** | The data type pandas gave a column: `str` for text, `float64` for decimals, `int64` for whole numbers. |
| **NaN** | How pandas shows a missing value. It's short for "Not a Number." |
| **Cell** | A small box of code in a notebook. Run it with Shift+Enter. |
| **Kernel** | The Python process behind a notebook. It keeps your variables between cells. |
| **Restart & Run All** | Start the kernel fresh and run every cell from the top. It proves the notebook works. |
| **Boolean filter** | A True/False condition inside `df[...]` that keeps only the rows where it's True. |
| **Duplicate** | A row that matches an earlier row exactly. |

## Before you read

A file of donations has 8 rows. One weight is blank, and one donation was typed in twice. You add up the weights without checking. What goes wrong?

<details>
<summary>Answer</summary>

The repeated donation gets counted twice, so the total is too high. The blank weight is skipped without warning, so you don't even know a donation is missing.

</details>

## Read

**[Start the reading: Look Before You Filter →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/pandas-inspect-filter/reading-1-lookbeforeyoufilter/)** (about 20 minutes)

As you read, look for:

1. What happens when you run a cell whose variable was never created.
2. Why one blank turns a whole-number column into `float64`.
3. Why each condition in a two-part filter needs its own parentheses.

## Main takeaways

### Summary

* **A notebook runs one cell at a time.** The kernel remembers what you ran, in the order you ran it. Use Restart & Run All before you share.
* **Check every new file four ways, every time.** Zero problems is still a finding: now you know the file is sound instead of hoping it is.
* **A boolean filter keeps rows where a condition is True.** Join two conditions with `&` (AND) or `|` (OR), each in its own parentheses. Filtering makes a new, smaller table and leaves the original alone.

| Check | Code | Question it answers |
| --- | --- | --- |
| Shape | `df.shape` | Did every row and column arrive? |
| Data types | `df.dtypes` | Is each column the type I expect? |
| Missing values | `df.isna().sum()` | How many blanks are in each column? |
| Duplicates | `df.duplicated().sum()` | Are any rows repeated? |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Shift+Enter runs the whole notebook." | It runs only the cell you're in. Restart & Run All runs everything. |
| "Checks are only for big files." | A blank or a repeat changes totals in a file of any size. |
| "Python's `and` joins two filter conditions." | pandas compares whole columns, so it uses `&`, with each condition in parentheses. |

### How this connects

* **Next quest:** You'll turn filtered rows into one summary per group, like total pounds for each site.
* **Boss Battle:** Part 1 of your project is exactly these four checks on your chosen dataset. Write down what each one finds.

## Quick check

**1.** Every weight in a file is a whole number, but `df.dtypes` shows `weight_lbs` as `float64`. Why?

<details>
<summary>Answer</summary>

At least one weight is blank. pandas stores a blank number as NaN, which is a decimal, so the whole column becomes `float64`.

</details>

**2.** Which line keeps only the rows where the site is Eastside **and** the category is Produce?

* A. `df[df["site"] == "Eastside" & df["category"] == "Produce"]`
* B. `df[(df["site"] == "Eastside") & (df["category"] == "Produce")]`
* C. `df[(df["site"] == "Eastside") and (df["category"] == "Produce")]`

<details>
<summary>Answer</summary>

**B.** Each condition is in its own parentheses, joined by `&`. A gives a `TypeError`, and C uses `and`, which doesn't work on whole columns.

</details>

---

**Next:** [Quest 2.3 — One Row Per Group](quest-03-group-columns.md)
