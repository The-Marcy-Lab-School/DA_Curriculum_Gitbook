# Overview of Module 2: Exploratory Data Analysis (Read FIRST)

**Time:** About 7 minutes

Read this page before anything else in Module 2. It's your map: what the module is about, the order of the pages, the new tools, and where you'll practice each skill. Come back to it whenever you want to see where you are.

## What this module is about

In this module, you'll learn **exploratory data analysis (EDA)**. EDA means getting to know a real, messy table of data before you say anything about it. Step by step, you'll learn to check a table for problems and clean it. Then you'll describe it with numbers and charts, find a pattern you can trust, and explain it to someone who will never read your code. At the end, the [Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project) asks you to do all of it on your own, with one real dataset.

## What the words mean

This GitBook uses a few game words. Here's what each one is:

| You'll see | What it is |
| --- | --- |
| **Quest** | One day's reading: a GitBook page plus the interactive reading it links to |
| **Practice Day** | A review day with no new reading |
| **Checkpoint** | Review and solo practice before the project |
| **Boss Battle** | The Module Project, where you use every skill from the module on one real dataset |

## Your route

| Day | Page | You'll learn to... |
| --- | --- | --- |
| 1 | [Module 2 Introduction](introduction.md) | See where this module fits: what you already know, what's new, and why it matters at work |
| 1 | [Quest 2.1 — The Loudest Number: Descriptive Statistics](quest-01-descriptive-statistics.md) | Pick the number that best shows the usual value, and measure how spread out the values are |
| 2 | [Quest 2.2 — Look Before You Filter: Inspecting and Filtering Data](quest-02-inspect-filter.md) | Load a file in a notebook, check it four ways, and keep only the rows you need |
| 3 | [Quest 2.3 — One Row Per Group: Grouping, New Columns, and Merging](quest-03-group-columns.md) | Summarize groups, add new columns, and combine two tables |
| 4 | [Quest 2.4 — Who's This Chart For? Exploratory vs. Explanatory Charts](quest-04-two-kinds-of-charts.md) | Pick a chart type on purpose, and polish a chart for someone else |
| 5 | [Quest 2.5 — Real Numbers, Wrong Story: Chart Best Practices](quest-05-chart-best-practices.md) | Catch charts that mislead, even when every number is real |
| 6 | [Practice Day: Review](practice-day-06.md) | Review the first five quests and check code an AI (artificial intelligence) tool wrote |
| 7 | [Quest 2.6 — Drop, Fill, or Flag: Missing Data](quest-06-missing-data.md) | Decide what to do with each missing value, and say why |
| 8 | [Quest 2.7 — Write It Once: Cleaning Functions](quest-07-cleaning-function.md) | Put your cleaning steps in one function you can reuse |
| 9 | [Quest 2.8 — Beneath the Total: Finding Patterns in Groups](quest-08-mining-a-pattern.md) | Find a pattern you can trust by splitting the data into groups |
| 10 | [Quest 2.9 — The Pattern Isn't the Proof: Asking Questions About Your Data](quest-09-clarifying-questions.md) | Ask clear questions about where data came from |
| 11 | [Quest 2.10 — Two Sets of Eyes: Checking AI on Charts](quest-10-ai-on-charts.md) | Check an AI's description of a chart, and an AI's chart ideas |
| 12 | [Quest 2.11 — Nobody Was in the Room: Writing for Stakeholders](quest-11-stakeholder-communication.md) | Write a README (the first page people see in a project) and a memo (a short note) that a stakeholder can act on. A **stakeholder** is a person who uses your answer to make a decision. |
| 13–14 | [Module 2 Checkpoint: Review and Solo Practice](checkpoint.md) | Find a pattern on your own, then review everything |
| 14 | [Module 2 Conclusion](conclusion.md) | See what you can do now, and how to talk about it |
| 15–19 | Boss Battle (Module Project) | Run the whole workflow on one real dataset. Your instructor will share the details. |

## New tools this module

A **tool** is anything analysts use to get work done. This module has two kinds:

* A Python **package** (also called a *library*) is a collection of code other people wrote. You install it once, then load it into your code with `import`. NumPy, pandas, and Matplotlib are packages.
* **Software** is a program you open and use, like VS Code. Jupyter notebooks are files that you open and run in software. You don't `import` them.

The picture below shows how these tools fit together.

![A concept map. VS Code is software, a program you open. It opens a Jupyter notebook, which is a file (.ipynb) that holds your code in cells. The code imports three Python packages: NumPy for math on many numbers, pandas for tables of data, and Matplotlib for charts. pandas is built on NumPy, and pandas draws charts with Matplotlib.](images/tools-map.svg)

Each tool is introduced on the quest page where you first use it, in a section named for what the tool is, like "New Python package: pandas."

| Tool | Kind | What it does | Introduced in |
| --- | --- | --- | --- |
| **NumPy** | Python package | Does math on many numbers at once | [Quest 2.1](quest-01-descriptive-statistics.md#new-python-package-numpy) |
| **Jupyter notebooks** | A kind of file, run in software like VS Code | Run code in small steps and see each result right below it | [Quest 2.2](quest-02-inspect-filter.md#new-file-type-jupyter-notebooks) |
| **pandas** | Python package | Load, check, clean, and summarize tables of data | [Quest 2.2](quest-02-inspect-filter.md#new-python-package-pandas) |
| **Matplotlib** | Python package | Draw charts and save them as images | [Quest 2.4](quest-04-two-kinds-of-charts.md#new-python-package-matplotlib) |

## Where you'll practice each skill

The [Module 2 Introduction](introduction.md#skills-youll-build) explains what each skill means. This table shows where you'll practice it.

| Skill | Where you'll practice |
| --- | --- |
| **Statistical Analysis** | Quests 2.1, 2.3, 2.8 |
| **Data Distributions & Shape** | Quests 2.1, 2.5, 2.10 |
| **Data Mining** | Quests 2.3, 2.8, Checkpoint |
| **Data Cleaning & Imputation** | Quests 2.2, 2.6, 2.7 |
| **Data Visualization** | Quests 2.4, 2.5 |
| **Critical Thinking** | Quests 2.5, 2.9, 2.11, Checkpoint |
| **Stakeholder Communication** | Quests 2.4, 2.11 |
| **AI as Critic** | Quest 2.10 |
| **AI Evaluation** | Practice Day, Quest 2.10, Checkpoint |
| **Presentations** | Boss Battle (Module Project) |

## How each quest page works

Every quest page has the same sections, in the same order. At the top, you'll see the total time and the step of the EDA workflow you're on. The total time counts both the GitBook page and the interactive reading.

1. **Quick recall**: something you already know that this reading builds on
2. **Introduction**: an example (often with a picture), the main takeaway, and why it matters at work
3. **Learning goals**: a list of what you'll be able to do
4. **New tool section** (only when there is one), named for what the tool is, like "New Python package: NumPy" or "New software: Git": what it's for, how you'll see it, and where to learn more
5. **Words to know**: the new terms, in plain words
6. **Before you read**: a question to think about first
7. **⭐ Read (REQUIRED)**: what to look for, then the link to the interactive reading (about 20 minutes)
8. **Main takeaways**: a summary, common mix-ups, and how it connects to the next reading and the Boss Battle (Module Project)
9. **Quick check**: two questions to test yourself

Submit each reading for credit when you finish it.

---

**Next:** [Module 2 Introduction](introduction.md)
