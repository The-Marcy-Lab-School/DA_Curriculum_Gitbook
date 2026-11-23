# Quest 2.2 — Look Before You Filter: Inspecting and Filtering Data (Day 2)

**Total time:** about 35 minutes

**EDA workflow:** **Inspect** → Clean → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

This is step 1. You learned some Explore tools first, in The Loudest Number. Now you'll start where real analysis starts: checking a new file.

## Introduction

Sometimes a total is wrong before you start adding. For example, a shop's sales sheet lists the same $200 order twice, because a cashier clicked Save two times. If you add up the sheet, the shop looks like it made $200 more than it really did.

In this reading, you'll learn how to:

* open a data file in a notebook
* check the file in four ways
* keep only the rows you need

**Main takeaway:** Check every new file before you filter it or add anything up. One blank or one repeated row can make every answer wrong.

**Why it matters at work:** Almost every data task starts the same way: load a file, check it, and then choose the rows you need. If you skip the checks, a wrong total can reach your manager, and no one will notice it's wrong.

## Learning goals

Check off each goal once you can do it.

- [ ] I can load a CSV file into a notebook and explain why the order I run cells in matters.
- [ ] I can run four checks on any new file: shape, data types, missing values, and duplicates.
- [ ] I can filter rows on one or two conditions and sort the result.

**Skills:** Data Cleaning & Imputation

## Quick recall

* Recall that when you run a `.py` file, Python does every line from top to bottom and shows only what you `print()`. You traced scripts like this in [Trace the Path](../module-01/quest-01-control-flow.md). A notebook works a little differently.
* Recall that a **class** describes one kind of thing, an **object** is one thing made from it, and a **method** is a function that belongs to the object, from [Meet the Objects](../module-01/quest-08-oop.md). pandas is built the same way.
* Recall that when one value is far bigger than the rest, the median describes a typical value better than the mean. You saw this with the $5,000 gift in [The Loudest Number](quest-01-descriptive-statistics.md).

## New tool: Jupyter notebooks

**What it's for:** A Jupyter notebook is a kind of **file** (its name ends in `.ipynb`), not a package you import. You open it in **software** such as VS Code, which runs it for you. A notebook splits your code into small boxes called cells. You run one cell at a time and see its result right under it, which fits the way analysts explore: ask one small question, look, then ask the next.

**How you'll see it in this reading:**

```python
# Cell 1: press Shift+Enter to run it
import pandas as pd
df = pd.read_csv("intake.csv")
df.shape

# A later cell: it can still use df
df.dtypes
```

**Code walkthrough:**

1. Each cell runs on its own when you click into it and press **Shift+Enter**.
2. After cell 1 runs, the **kernel** (the Python program behind the notebook) remembers `pd` and `df`, so a later cell can use them.
3. A cell shows the value of its last line right under it, so `df.shape` shows up without `print()`.

Notebooks are for exploring. Finished programs are still `.py` files. If VS Code asks you to install `ipykernel`, click **Install**: it's the piece that connects VS Code to Python.

**Learn more:** [Jupyter Notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) (official guide for the editor you'll use) · [Jupyter: Get started](https://docs.jupyter.org/en/latest/start/index.html) (official: what notebooks and kernels are)

## New tool: pandas

**What it's for:** pandas is a free Python package for working with tables of data, like a spreadsheet you control with code. It loads a whole file in one line, and because every step is code, you can run the same checks again on next month's file.

**How you'll see it in this reading:**

```python
import pandas as pd  # load the package
df = pd.read_csv("intake.csv")
df.shape
df["site"] == "Eastside"
df.sort_values("weight_lbs", ascending=False)
```

**Code walkthrough:**

1. `import pandas as pd` loads the pandas package and gives it the short name `pd`.
2. `pd.read_csv("intake.csv")` is a pandas **function**. It reads the CSV file and gives back a **DataFrame**, pandas' table. `DataFrame` is a **class**, and `df` is one **object** made from it, just like the objects you made from your own classes.
3. `df.shape` is an **attribute**: a value stored on the object. It has no parentheses because you're reading a fact, not running an action. It gives two numbers: rows, then columns.
4. `df["site"] == "Eastside"` gives back a **Series**: one column with a `True` or `False` for each row. Is this row's site Eastside?
5. `df.sort_values(...)` is a **method**: a function that belongs to the object, so it has parentheses. It puts the rows in order by weight. Here, the parameter `ascending` is set to `False`, so the biggest weight comes first. (*Ascending* means smallest to biggest.)

If `import pandas` gives a `ModuleNotFoundError` on your laptop, run `pip install pandas` in the terminal once.

**Learn more:** [pandas: Getting started tutorials](https://pandas.pydata.org/docs/getting_started/intro_tutorials/index.html) (official, short, with pictures) · [W3Schools: pandas tutorial](https://www.w3schools.com/python/pandas/default.asp) · [W3Schools: pandas DataFrames](https://www.w3schools.com/python/pandas/pandas_dataframes.asp)

## Words to know

### Notebooks

| Word | What it means |
| --- | --- |
| **Notebook** | A file ending in `.ipynb` that holds code in cells, with each cell's result shown under it. |
| **Cell** | A small box of code in a notebook. Run one cell at a time with Shift+Enter. |
| **Kernel** | The Python process behind a notebook. It keeps your variables in memory between cells. It knows what you ran, in the order you ran it, not the order on the page. |
| **Restart & Run All** | Restart the kernel, then run every cell from top to bottom. It proves the notebook works from a clean start. |

{% hint style="info" %}
**Before you share a notebook, use Restart & Run All.** A notebook can seem to work only because of a cell you ran earlier and then deleted. A clean run from the top catches that.
{% endhint %}

### Tables in pandas

| Word | What it means |
| --- | --- |
| **CSV file** | A plain text file of a table. Each line is a row, commas separate the columns, and the first line holds the column names. |
| **DataFrame** | pandas' table: a class with rows and named columns, where each column has its own data type. Each table you load is a DataFrame object. |
| **Series** | One column of a DataFrame: a list of values with row labels. Picking a column, like `df["site"]`, gives you a Series. |
| **dtype** | The data type pandas gave a column: `str` for text, `int64` for whole numbers, `float64` for decimal numbers. Older tutorials and AI answers say `object` for text. That's the old label. |
| **NaN** | How pandas shows a missing value. It's short for "not a number," but pandas stores it as a decimal number. |

### The four checks

Run these on every new file, before you do anything else.

| Check | What it means | Units |
| --- | --- | --- |
| **Shape** | How big the table is: did every row and column arrive? | Two counts: rows first, then columns |
| **Data types** | The dtype of each column: is each one the type you expect? | A label per column, not a number |
| **Missing values** | How many cells are blank in each column. | A count of blank cells, per column |
| **Duplicate** | A row that matches an earlier row exactly, in every column. A donation logged twice adds its weight twice. | A count of rows |

A count can show as `np.int64(1)`. That's just a whole number, stored the NumPy way.

![A flow from top to bottom. First, load a new file with pd.read_csv. Then run four checks in order. 1, Shape: did every row arrive? df.shape. 2, Data types: is each column the right type? df.dtypes. 3, Missing values: where are the blanks? df.isna().sum(). 4, Duplicates: do any rows repeat? df.duplicated().sum(). Only then filter to keep the rows you need.](images/four-checks.svg)

### Keeping and ranking rows

| Word | What it means |
| --- | --- |
| **Boolean** | A value that is either `True` or `False`. |
| **Boolean filter** | A True/False condition inside `df[...]` that keeps only the rows where it's True. The result is a new, smaller DataFrame. The original stays the same. |
| **`&` (AND)** | How pandas joins two filter conditions so that both must be True. It narrows the result: you keep fewer rows. Each condition goes in its own parentheses. |
| **Sort** | Put the rows in order by one column. Filtering picks rows. Sorting ranks them. |

The partner of `&` is `|`, which means OR. It keeps a row if either condition is True, so it widens the result.

## Before you read

In the reading, you'll focus on a food bank's donation file. Each row is one donation: who gave it, what kind of food, how much it weighed, and which site got it. The manager asks, "How much produce came into Eastside?"

Think about: before you add up any weights, what could be wrong in the file that would make your total wrong? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. What happens when you run a cell whose variable was never created.
2. Why one blank turns a whole-number column into `float64`.
3. Why each condition in a two-part filter needs its own parentheses.

**[Start the reading: Look Before You Filter →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/pandas-inspect-filter/reading-1-lookbeforeyoufilter/)** (about 20 minutes)

## Main takeaways

### Summary

* **A notebook runs one cell at a time.** The kernel remembers what you ran, in the order you ran it. Use Restart & Run All before you share.
* **Check every new file four ways, every time:** shape (`df.shape`), data types (`df.dtypes`), missing values (`df.isna().sum()`), and duplicates (`df.duplicated().sum()`). Write down what each one finds. Zero problems is still a finding: now you know the file is sound instead of hoping it is.
* **A boolean filter keeps rows where a condition is True.** Join two conditions with `&` (AND) or `|` (OR), each in its own parentheses. Count duplicates before you rank or total anything, because a repeated row can take two top spots.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Shift+Enter runs the whole notebook." | It runs only the cell you're in. Restart & Run All runs everything. |
| "Checks are only for big files." | A blank or a repeat changes totals in a file of any size. |
| "Filtering changes my table." | It makes a new, smaller table. After `eastside = df[df["site"] == "Eastside"]`, `df` still has all 8 rows. |
| "Python's `and` joins two filter conditions." | pandas compares whole columns, so it uses `&`, with each condition in parentheses. |
| "Text columns should say `object`." | That's the old label. pandas 3 shows text as `str`. If a number column shows `str`, something in it isn't a clean number, like `"12 lbs"`. |

### How this connects

* **Next reading:** Instead of keeping one group of rows at a time, you'll split all the rows into groups and get one summary number for each group, such as total pounds for each site. You'll also add new columns and bring in columns from a second table.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** When you get a real dataset, you'll start with these same four checks and write down what each one finds before you analyze anything.

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

**Next:** [Quest 2.3 — One Row Per Group: Grouping, New Columns, and Merging (Day 3)](quest-03-group-columns.md)
