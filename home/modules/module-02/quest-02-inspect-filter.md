# Quest 2.2 — Look Before You Filter: Inspecting and Filtering Data (Day 2)

**Total time:** About 40 minutes

**EDA workflow:** **Inspect** → Clean → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Quick recall

**Why Inspect now?** In [The Loudest Number](quest-01-descriptive-statistics.md), you found the mean, the median, and the spread of a short list of gifts. You could see every value at once. In [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md), your function checked one record at a time and caught blank values. A real file can have thousands of rows, and you can't see them all. So now you go back to step 1, where real analysis starts. You check the whole file before you trust any mean or median. In the next quest, you'll build on this. You'll make one summary for each group of rows, like the total pounds of food at each site. ([Why the quests don't follow the step order](introduction.md#why-the-quests-dont-follow-the-step-order))

* In Module 0's [Meet Your Terminal](../module-00/quest-01-terminal.md), you looked before you moved in a new folder: `pwd` and `ls` first, then `cat` to print a file. A new data file gets the same habit: look first, then act.
* Every column has a data type. In Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), you named each one, and stored an ID like `00417` as text so it keeps its zeros.
* Your validation function in Module 1's [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md) checked each record before you used it. It checked the shape first (the right number of fields?), then the values (is the grade made of digits?).

## Introduction

Sometimes a total is wrong before you start adding. For example, a shop makes sales of $50, $120, $200, and $80 in one morning. The real total is $50 + $120 + $200 + $80 = **$450**.

But a cashier clicked Save two times on the $200 sale, so the sales sheet lists it twice. Now the sheet adds up to $450 + $200 = **$650**. The shop looks like it made $200 more than it really did. Now look at the red row on the left sheet in the picture below.

![Two sales sheets. Left, one sale saved twice: the rows are $50, $120, $200, $200, and $80, and the repeated $200 row is red. Total = $50 + $120 + $200 + $200 + $80 = $650, which is $200 more than the shop made. Right, each sale listed once: $50, $120, $200, and $80. Total = $50 + $120 + $200 + $80 = $450, which matches the real sales.](images/duplicate-sale-total.svg)

**Main takeaway:** Inspect every new file before you filter it or add anything up. To **inspect** a file means to run four checks on it:

* **Shape:** did every row and column arrive?
* **Data types:** is each column the type you expect?
* **Missing values:** where are the blanks?
* **Duplicates:** do any rows repeat?

One **duplicate**, a row that repeats an earlier row, adds its value twice, like the $200 sale.

**Why it matters at work:** Analysts check every new file so the totals, counts, and rankings they report are right. For example, analysts check a file before they:

* add up a month of sales for a report
* count how many new customers signed up
* rank the top five best-selling products

If you skip the checks, a wrong total can reach your manager, and no one will notice it's wrong.

## Learning goals

After this reading, you should be able to say:

* I can load a CSV (comma-separated values) file into a notebook and explain why the order I run cells in matters.
* I can run four checks on any new file:
  - shape
  - data types
  - missing values
  - duplicates
* I can filter rows on one or two conditions and sort the result.

**Skills:** Data Cleaning & Imputation

## New file type: Jupyter notebooks

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

<details>
<summary>Expand to walk through the code</summary>

1. Each cell runs on its own when you click into it and press **Shift+Enter**.
2. After cell 1 runs, the **kernel** (the Python program behind the notebook) remembers `pd` and `df`, so a later cell can use them.
3. A cell shows the value of its last line right under it, so `df.shape` shows up without `print()`.

</details>

Notebooks are for exploring. Finished programs are still `.py` files. If VS Code asks you to install `ipykernel`, click **Install**: it's the piece that connects VS Code to Python.

**Learn more:** [Jupyter Notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) (official guide for the editor you'll use) · [Jupyter: Get started](https://docs.jupyter.org/en/latest/start/index.html) (official: what notebooks and kernels are)

## New Python package: pandas

**What it's for:** pandas is a free Python package for working with tables of data, like a spreadsheet you control with code. It loads a whole file in one line, and because every step is code, you can run the same checks again on next month's file.

pandas holds a table in a **DataFrame**, and one column of it in a **Series**. Compare them to what you already know:

| | What you know | pandas version |
| --- | --- | --- |
| **A whole table** | A CSV file, like `pets.csv`. In Python, a list of dictionaries, one per row: `[{"item": "Mug", "amount": 50}, ...]` | A **DataFrame**: rows and named columns in one object, `df`. Each column has one data type. |
| **One column** | A list of values, like `amounts = [50, 120, 200]`. You find an item by its position: `amounts[0]` is `50`. | A **Series**: the column's values, plus a label for each row. `df["amount"]` gives you one. |
| **Example: `== 200`** | `[50, 120, 200] == 200` compares the whole list to one number, so it gives just `False`. | `df["amount"] == 200` checks every row, so it gives a `True` or `False` for each one. That's how filters work. |

**How you'll see it in this reading:**

```python
import pandas as pd  # load the package
df = pd.read_csv("intake.csv")
df.shape
df["site"] == "Eastside"
df.sort_values("weight_lbs", ascending=False)
```

<details>
<summary>Expand to walk through the code</summary>

1. `import pandas as pd` loads the pandas package and gives it the short name `pd`.
2. `pd.read_csv("intake.csv")` is a pandas **function**. It reads the CSV file and gives back a **DataFrame**, pandas' table. In [Make It Survive](../module-01/quest-05-serialization.md), you loaded a saved file and then checked the type of each value, because loading can change types. `read_csv` loads a whole table in one line, and `df.dtypes` does that type check for every column. `DataFrame` is a **class**, and `df` is one **object** made from it, just like the objects you made from your own classes in [Meet the Objects](../module-01/quest-08-oop.md).
3. `df.shape` is an **attribute**: a value stored on the object. It has no parentheses because you're reading a fact, not running an action. It gives two numbers: rows, then columns.
4. `df["site"] == "Eastside"` gives back a **Series**: one column with a `True` or `False` for each row. Is this row's site Eastside?
5. `df.sort_values(...)` is a **method**: a function that belongs to the object, so it has parentheses. It puts the rows in order by weight. Here, the parameter `ascending` is set to `False`, so the biggest weight comes first. (*Ascending* means smallest to biggest.)

</details>

If `import pandas` gives a `ModuleNotFoundError` on your laptop, run `pip install pandas` in the terminal once.

**Learn more:** [pandas: Getting started tutorials](https://pandas.pydata.org/docs/getting_started/intro_tutorials/index.html) (official, short, with pictures) · [W3Schools: pandas tutorial](https://www.w3schools.com/python/pandas/default.asp) · [W3Schools: pandas DataFrames](https://www.w3schools.com/python/pandas/pandas_dataframes.asp)

## Words to know

The examples on this page use the shop's sales sheet from the Introduction, saved as the file `sales.csv`. It has the same 5 rows, with the $200 sale saved twice. This page adds two columns:

* `payment`: how the customer paid
* `cashier`: who made the sale

One payment was never written down.

| item | amount | payment | cashier |
| --- | --- | --- | --- |
| Mug | 50 | Cash | Jo |
| Lamp | 120 | Card | Sam |
| Chair | 200 | Card | Jo |
| Chair | 200 | Card | Jo |
| Rug | 80 | *(blank)* | Sam |

The 4th row repeats the 3rd row. That's the $200 sale saved twice.

### Notebooks

| Word | What it means | Example with the sales sheet |
| --- | --- | --- |
| **Notebook** | A file ending in `.ipynb` that holds code in cells, with each cell's result shown under it. | `sales.ipynb` |
| **Cell** | A small box of code in a notebook. Run one cell at a time with Shift+Enter. | A cell that holds only `df.shape` |
| **Kernel** | The Python process behind a notebook. It keeps your variables in memory between cells. It knows what you ran, in the order you ran it, not the order on the page. | In a fresh kernel, `df.shape` gives a `NameError`, because `df` doesn't exist yet. |
| **Restart & Run All** | Restart the kernel, then run every cell from top to bottom. It proves the notebook works from a clean start. | It catches a notebook whose `pd.read_csv("sales.csv")` cell was deleted after it ran. |

{% hint style="info" %}
**Before you share a notebook, use Restart & Run All.** A notebook can seem to work only because of a cell you ran earlier and then deleted. A clean run from the top catches that.
{% endhint %}

### Tables in pandas

| Word | What it means | Example with the sales sheet |
| --- | --- | --- |
| **CSV file** | A plain text file of a table. Each line is a row, commas separate the columns, and the first line holds the column names. | `sales.csv`. One row: `Mug,50,Cash,Jo` |
| **DataFrame** | pandas' table: a class with rows and named columns, where each column has its own data type. Each table you load is a DataFrame object. | `df`, with 5 rows and 4 columns |
| **Series** | One column of a DataFrame: a list of values with row labels. Picking a column, like `df["payment"]`, gives you a Series. | `df["payment"]`: Cash, Card, Card, Card, NaN |
| **dtype** | The data type pandas gave a column: `str` for text, `int64` for whole numbers, `float64` for decimal numbers. Older tutorials and AI (artificial intelligence) answers say `object` for text. That's the old label. | `payment` is `str`. `amount` is `int64`. |
| **NaN** | How pandas shows a missing value. It's short for "not a number," but pandas stores it as a decimal number. | The payment for the Rug sale |

### The four checks

To **inspect** a file means to run these four checks on it, before you do anything else.

**Units** are what a number counts, like rows or blank cells. Each check gives a count, except data types, which gives a label for each column. The examples use the sales sheet, `sales.csv`.

| Check | What it means | Example with the sales sheet |
| --- | --- | --- |
| **Shape** | How big the table is: did every row and column arrive? | `df.shape` gives **(5, 4)**: 5 rows, then 4 columns |
| **Data types** | The dtype of each column: is each one the type you expect? | `df.dtypes`: `amount` is **`int64`**. The other 3 columns are **`str`**. |
| **Missing values** | How many cells are blank in each column. | `df.isna().sum()`: **1 blank cell** in `payment`, 0 in the rest |
| **Duplicate** | A row that matches an earlier row exactly, in every column. A sale saved twice adds its amount twice. | `df.duplicated().sum()`: **1 row**, the second `Chair,200,Card,Jo` |

A count can show as `np.int64(1)`. That's just a whole number, stored the NumPy way.

You've done each check before, by hand, on one record or one value at a time:

* **Shape:** your validation function checked that each line had the right number of fields, in [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md).
* **Data types:** you named each column's data type, and kept IDs as text, in [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md).
* **Missing values:** `"".isdigit()` is `False`, so your validation function caught a blank grade, in [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md).
* **Duplicates:** a set keeps each value only once, in [Pick the Right Container](../module-01/quest-04-data-structures.md).

pandas runs each check on the whole table in one line. The picture below shows the four checks in order, with the filter last.

![A flow from top to bottom. First, load a new file with pd.read_csv. Then run four checks in order. 1, Shape: did every row arrive? df.shape. 2, Data types: is each column the right type? df.dtypes. 3, Missing values: where are the blanks? df.isna().sum(). 4, Duplicates: do any rows repeat? df.duplicated().sum(). Only then filter to keep the rows you need.](images/four-checks.svg)

### Keeping and ranking rows

| Word | What it means | Example with the sales sheet |
| --- | --- | --- |
| **Boolean** | A value that is either `True` or `False`. | `"Card" == "Card"` is `True` |
| **Boolean filter** | A True/False condition inside `df[...]` that keeps only the rows where it's True. The result is a new, smaller DataFrame. The original stays the same. | `df[df["payment"] == "Card"]` keeps **3** of the 5 rows |
| **`&` (AND)** | How pandas joins two filter conditions so that both must be True. It narrows the result: you keep fewer rows. Each condition goes in its own parentheses. | Card **and** Sam keeps **1** row: the Lamp sale |
| **Sort** | Put the rows in order by one column. Filtering picks rows. Sorting ranks them. | Biggest first: **$200, $200, $120**. The repeated sale takes two top spots. |

The partner of `&` is `|`, which means OR. It keeps a row if either condition is True, so it widens the result. Card **or** Sam keeps **4** rows.

## Before you read

In the reading, you'll focus on a food bank's donation file. A **food bank** is a group that collects food and gives it to people who need it. Each row is one donation: who gave it, what kind of food, how much it weighed, and which site (location) got it. The manager asks, "How much produce (fresh fruits and vegetables) came into Eastside?"

Think about: before you add up any weights, what could be wrong in the file that would make your total wrong? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. What happens when you run a cell whose variable was never created.
2. Why one blank turns a whole-number column into `float64`.
3. Why each condition in a two-part filter needs its own parentheses.

**[Start the reading: Look Before You Filter →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/pandas-inspect-filter/reading-1-lookbeforeyoufilter/)** (about 20 minutes)

## Main takeaways

### Summary

* **A notebook runs one cell at a time.** The kernel remembers what you ran, in the order you ran it. Use Restart & Run All before you share.
* **Check every new file four ways, every time.** Write down what each one finds. Zero problems is still a finding: now you know the file is fine, instead of hoping it is.
  * Shape: `df.shape`
  * Data types: `df.dtypes`
  * Missing values: `df.isna().sum()`
  * Duplicates: `df.duplicated().sum()`
* **A boolean filter keeps rows where a condition is True.** Join two conditions with `&` (AND) or `|` (OR), each in its own parentheses. Count duplicates before you rank or total anything, because a repeated row can take two top spots.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Shift+Enter runs the whole notebook." | It runs only the cell you're in. Restart & Run All runs everything. |
| "This sheet has only 5 rows. I can see it's fine, so I'll skip the checks." | The 5-row sales sheet has 1 blank payment and 1 repeated row. The repeat adds an extra $200: the total is $650 instead of $450. |
| "Filtering changes my table." | It makes a new, smaller table. After `card = df[df["payment"] == "Card"]`, `df` still has all 5 rows. |
| "I can join two filter conditions with `and`, like in an `if` statement." | pandas compares whole columns, so it uses `&`, with each condition in parentheses. Without the parentheses, you get a `TypeError`. |
| "My text columns show `str`. A tutorial said they should say `object`, so something's wrong." | That's the old label. pandas 3 shows text as `str`. If a number column shows `str`, something in it isn't a clean number, like `"$50"`. |

### How this connects

* **Next reading:** Instead of keeping one group of rows at a time, you'll split all the rows into groups and get one summary number for each group, such as total pounds for each site. You'll also add new columns and bring in columns from a second table.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** When you get a real dataset, you'll start with these same four checks and write down what each one finds before you analyze anything.

## Quick check

**1.** Every amount on a sales sheet is a whole number, but `df.dtypes` shows `amount` as `float64`. Why?

<details>
<summary>Answer</summary>

At least one amount is blank. pandas stores a blank number as NaN, which is a decimal, so the whole column becomes `float64`.

</details>

**2.** Which line keeps only the rows where the payment is Card **and** the cashier is Sam?

* A. `df[df["payment"] == "Card" & df["cashier"] == "Sam"]`
* B. `df[(df["payment"] == "Card") & (df["cashier"] == "Sam")]`
* C. `df[(df["payment"] == "Card") and (df["cashier"] == "Sam")]`

<details>
<summary>Answer</summary>

**B.** Each condition is in its own parentheses, joined by `&`. A gives a `TypeError`, and C uses `and`, which doesn't work on whole columns.

</details>

---

**Next:** [Quest 2.3 — One Row Per Group: Grouping, New Columns, and Merging (Day 3)](quest-03-group-columns.md)
