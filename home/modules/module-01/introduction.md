# Module 1 Introduction: Programming Fundamentals

**Time:** about 15 minutes

## Where you've been

You already have the habits this module builds on:

* **Understand data:** You can tell what kind of data a column holds, and you know that "made of digits" doesn't always mean "a number."
* **Use the terminal:** You can move between folders and run commands.
* **Save with Git:** You save your work in small steps and share it on GitHub.
* **Verify claims:** You check an AI's answer before you trust it.

Now you'll start writing your own programs.

## Where you're going

In this module, you'll learn Python, the programming language you'll use for the rest of the program. You'll write programs that make decisions, repeat steps, organize work into functions, hold data in the right container, save data to files, and keep going when the data is bad. You'll also learn to predict what code will do before you run it, and to find bugs when it doesn't.

## What is Python?

**Code** is a set of written instructions for a computer. A **program** is a set of instructions that a computer follows in order, from top to bottom. **Python** is a **programming language**: a way of writing those instructions so that both people and computers can read them.

Here's a tiny Python program:

```python
prices = [4.50, 3.25, 6.00]
total = sum(prices)
print(total)
```

**Code walkthrough:**

1. `prices = [4.50, 3.25, 6.00]` stores three prices in a list named `prices`.
2. `total = sum(prices)` adds them up and stores the answer in `total`.
3. `print(total)` shows the answer on the screen: `13.75`.

You save code like this in a file that ends in `.py`. Then you run it from the terminal. Python reads your code one line at a time, from top to bottom, and does what each line says.

![A flow from left to right. 1: you write code in a .py file, like prices.py. 2: you run it in the terminal by typing python3 prices.py. 3: Python reads it one line at a time, top to bottom. 4: you see the result, 13.75. If a line breaks Python's rules, its syntax, Python stops and shows an error instead.](images/m1-python-runs.svg)

## Why data professionals use Python

Imagine you need to check 10,000 rows of sales data for missing prices. By hand, that could take days, and you'd probably miss some. A Python program can check every row in seconds, the same way every time. That's the main reason analysts use Python: it **repeats work on many records automatically**.

Python is also a good fit for data work because:

* **It's readable.** Python code looks close to plain English, so teammates can check your steps.
* **It's free and widely used.** Python is one of the most common languages in data jobs, so it shows up in job postings and interviews.
* **It has packages for data.** A **package** is a collection of code that other people wrote, which you can load into your own program. In the next module, you'll use packages for tables of data, statistics, and charts.
* **It makes your work repeatable.** Next month, you can run the same program on the new data, and get the same steps again. Someone else can rerun it to check your work.

In this module, you'll learn plain Python first, without packages. Every package you use later is built from the same pieces you learn here: decisions, loops, functions, lists, dictionaries, classes, and error handling.

## Python syntax and style

Python has two kinds of rules. One kind is required. The other is a shared habit that makes code easier for people to read.

### Syntax: the rules Python must have

**Syntax** is the set of grammar rules for how code must be written so Python can read it. If you break a syntax rule, Python stops and shows an error. Nothing after that point runs.

Here's an example. An `if` line must end with a colon (`:`):

```python
price = 6
if price > 5
    print("expensive")
```

Python stops and shows:

```text
SyntaxError: expected ':'
```

In Python, **indentation** (the spaces at the start of a line) is also syntax. The lines that belong inside an `if`, a loop, or a function must be indented. If they aren't, you'll see an `IndentationError`.

### Style: PEP 8, the rules people expect

**PEP 8** is Python's official **style guide**. A style guide is a set of shared habits for writing code that's easy to read. (PEP stands for "Python Enhancement Proposal," a document that describes an idea for Python.)

Code that breaks PEP 8 still runs. But it's harder for people to read, and teams at work expect PEP 8. Here are the rules you'll use most:

| PEP 8 rule | Example |
| --- | --- |
| Name variables and functions in `snake_case`: lowercase words joined by underscores | `total_price`, `def clean_row():` |
| Name classes in `CapWords`: each word starts with a capital letter | `class InventoryItem:` |
| Name values that never change in `UPPER_CASE` | `MAX_ITEMS = 100` |
| Indent with 4 spaces | `    print(total)` |
| Put one space on each side of `=` and math signs | `total = price * 2` |
| Don't put spaces around `=` inside a function call | `round(total, ndigits=2)` |
| Keep lines short, at most 79 characters | Split a long line into two |

These two lines do the same thing. Only the second follows PEP 8:

```python
TotalPrice=Price*2+Tax       # runs, but hard to read
total_price = price * 2 + tax  # follows PEP 8
```

### Syntax or style?

| | Syntax | Style (PEP 8) |
| --- | --- | --- |
| **What it is** | The rules Python requires | The habits people expect |
| **If you break it** | Python stops with an error | The code runs, but it's harder to read |
| **Example** | A missing colon after `if` | A variable named `TotalPrice` |

**Learn more:** [PEP 8: Style Guide for Python Code](https://peps.python.org/pep-0008/) (official) · [W3Schools: Python Syntax](https://www.w3schools.com/python/python_syntax.asp) · [W3Schools: Python Introduction](https://www.w3schools.com/python/python_intro.asp) · [The Python Tutorial](https://docs.python.org/3/tutorial/index.html) (official)

## The big picture: the building blocks of a data program

Every program you write in this module is made of the same five building blocks. Each quest (one or two readings) teaches one of them:

![A concept map of five building blocks around a data program written in Python. Decide and repeat: if statements and loops, Quest 1.1. Organize steps: functions, Quests 1.2 and 1.7. Hold data: lists, dictionaries, and objects, Quests 1.4 and 1.8. Load, save, and protect: files, validation, and errors, Quests 1.5 and 1.6. Check your work: speed and debugging, Quests 1.3, 1.9, and 1.10.](images/m1-building-blocks.svg)

| Building block | The question it answers |
| --- | --- |
| **Decide and repeat** | How does my program choose what to do, and do it for every record? |
| **Organize steps** | How do I write a step once and use it again? |
| **Hold data** | Which container fits my data: a list, a dictionary, or my own object? |
| **Load, save, and protect** | How do I read and save files, and keep going when the data is bad? |
| **Check your work** | Will my program stay fast as the data grows? Does it give the right answer? |

The building blocks aren't steps in a set order. A real program uses all five at once. At the top of every quest page, you'll see which block you're on, like this:

**Building blocks:** Decide and repeat · **Organize steps** · Hold data · Load, save, and protect · Check your work

## What you'll be able to do

By the end of this module, you'll be able to:

* **Decide and repeat:** Write `if` statements and loops, and trace what they'll print before you run them.
* **Organize steps:** Write functions with parameters and return values, and explain where each variable can be used.
* **Hold data:** Pick a list, tuple, set, or dictionary for a job. Build your own class and create objects from it.
* **Load, save, and protect:** Save data to a file and load it back. Check incoming data, and handle errors so one bad record doesn't stop your program.
* **Check your work:** Explain how a program slows down as the data grows. Find and fix a bug, and prove that code that runs isn't always correct.

## Skills you'll build

These are the skills employers look for. The names in bold are the official skill names you'll see on your readings and your project's grading guide. The Boss Battle (Module Project) checks the first five.

| Group | Skill | What it means |
| --- | --- | --- |
| **Writing programs** | **Control Flow & Loops** | Make a program choose and repeat |
| | **Functions & Modular Programming** | Break work into small, reusable functions |
| | **Object-Oriented Programming** | Build your own classes and objects |
| **Making programs fast** | **Algorithmic Complexity (Big-O)** | Explain how a program's speed changes as the data grows |
| **Making programs correct** | **Attention to Detail** | Check edge cases, handle bad data, find bugs, and make sure the output is right |
| **Practiced in the readings** | **Data Structures & Algorithms** | Pick the right container for your data, and know how fast it is to search |

## The Boss Battle (Module Project)

At the end of this module, you'll build a real program in plain Python: an **inventory tracker** for a business. It reads a list of transactions, like items coming in and going out, and keeps track of what's in stock.

Real data is messy, so your program will have to check every transaction, skip bad lines without crashing, and report which items are running low. You'll use every building block: decisions and loops, functions, the right containers, your own class, files, and error handling. You'll also explain why a dictionary lookup is faster than searching a list.

When you finish, you'll have a working program that you built yourself, and you'll be able to explain every line of it. Your instructor will share the exact requirements when the project starts.

---

**Next:** [Quest 1.1 — Trace the Path: Conditionals and Loops (Days 1–2)](quest-01-control-flow.md)

Need the map again? Go back to the [Overview of Module 1 (Read FIRST)](overview.md).
