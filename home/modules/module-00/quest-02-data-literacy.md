# Quest 0.2 — What Kind of Data Is This? Data Types and Data Structures (Day 1)

**Total time:** About 35 minutes

**Analyst toolkit:** Use the terminal · **Understand data** · Save with Git · Verify claims ([what's this?](introduction.md#the-big-picture-your-analyst-toolkit))

## Introduction

Some numbers are not really numbers. For example, your phone number is made of digits. But you would never add two phone numbers together, or find the average phone number. A phone number is a label, not an amount.

A computer can't tell the difference on its own. You have to tell it what kind of value each piece of information is.

**Main takeaway:** Choose a value's **data type** by what the value means, not by what it looks like. A data type is what kind of value something is, like text or a whole number. If you would never do math with a value, store it as text, even when it's made of digits.

**Why it matters at work:** Analysts use data types to decide what they can do with each column of data. For example, they use them to:

* keep a customer ID as text, so `00417` doesn't turn into `417`. A customer ID (short for identifier) is a code that labels one customer.
* pick which columns to add up or average, like prices, and which to leave alone, like ZIP codes
* store dates as dates, so they can count the days between two of them

If a column has the wrong data type, the data changes with no warning. Then `417` may match the wrong customer.

## Learning goals

After this reading, you should be able to say:

* I can explain the difference between a variable and its value.
* I can name the data type of a value, and explain why an ID made of digits should be stored as text.
* I can explain the difference between a data type and a data structure.

**Skills:** Data Literacy · General Programming & Coding

## Quick recall

* In [Meet Your Terminal](quest-01-terminal.md), `ls` listed what's inside a folder, and `cat` printed a file on the screen. The reading starts with two warm-up questions about them.
* A ZIP code is made of digits, but the [Module 0 Introduction](introduction.md#why-this-matters-for-data-work) showed it names a place, not an amount. Some start with zeros, like `00501`, and dropping them would send the mail to the wrong place.
* Your phone already groups values: one contact holds a name, a phone number, and an email together. A data structure works the same way.

## Words to know

### What is it called?: Variables and values

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Variable** | A named container that holds a value. The value can change. Think of a box with a label on it. | `pet_of_the_week` |
| **Value** | The piece of information inside a variable right now. | `"Mango"` or `12.5` |
| **`=` (store)** | In code, `=` means "store this value in this variable." It does not mean "is equal to," like in math. | `pet_of_the_week = "Biscuit"` |
| **Quotes `" "`** | Quotes around a value mark it as text. | `"00417"` is text. `00417` without quotes is a number. |

### What kind of value is it?: Data types

A **data type** is what kind of value something is. The reading uses plain names. Python, the language you'll write code in later, has its own short name for most of them, so you'll see both.

| Plain name | Python's name | Example in the reading | Can you do math with it? |
| --- | --- | --- | --- |
| **Text** | **String** (`str`) | a pet's name, `"Biscuit"` | No |
| **Whole number** | **Integer** (`int`) | a pet's age, `3` | Yes |
| **Decimal** | **Float** (`float`) | a weight in pounds, `12.5` | Yes |
| **True/false** | **Boolean** (`bool`) | has this pet been adopted? `True` | No (it's a yes or no) |
| **Date** | a date type (you'll meet it later) | the day a pet arrived, `2026-09-14` | Only date math, like days between two dates: `2026-10-02` − `2026-09-14` = **18 days** |

| Word | What it means |
| --- | --- |
| **Identifier (ID)** | A value that names or labels one thing, like a pet's tag number (the number on the small label each pet wears), a student ID, or a ZIP code. It can be made of digits, but you never do math with it. Store it as text. |
| **Leading zero** | A zero at the start of a value, like the first two zeros in `00417`. A whole number drops them, so `00417` becomes `417`. |
| **Quantitative** | Describes a value that measures an amount, so math makes sense: an age, a weight, a price. An ID is not quantitative, even when it's made of digits. |

The picture below shows the tag number `00417` stored two ways. Compare what the computer keeps in each panel.

![Two panels side by side for the pet tag number 00417. Left, stored as text: you enter "00417" and the computer keeps 00417, so it still matches the right pet. Right, stored as a whole number: you enter 00417 and the computer keeps 417, so the first zeros are gone and it looks like tag 417. A rule underneath says: if you would never do math with it, store it as text.](images/m0-tag-number.svg)

### How are values grouped?: Data structures

| Word | What it means | Example |
| --- | --- | --- |
| **Data structure** | A way to group several values together as one unit. | One pet's row is a small one. The whole file of pets is a bigger one. |
| **Record** | One row of data about one thing. | `Mango,1,4.2,False,2026-10-02` |
| **Column** | One kind of information that every record has. A column's values usually share one data type. | `age`, with the whole numbers `3`, `1`, and `7` |
| **CSV file** | A plain text file that holds a table. CSV stands for "comma-separated values." The first line holds the column names. Each line after it is one record. Commas separate the values. | `pets.csv`, whose first line is `name,age,weight,adopted,arrived` |
| **Structured data** | Data that sits in rows and columns, with the same columns for every row. | `pets.csv` |
| **Unstructured data** | Data with no rows or columns. | A paragraph of free text, an email, or a photo |

You'll need *structured* and *unstructured* again in a later quest. The required reading doesn't cover them, but the optional reading near the end of this page does.

The picture below puts three ideas side by side. Read the panels from left to right: a variable, a data type, then a data structure.

![Three panels. Variable, a labeled box: the box pet_of_the_week holds "Biscuit" in week 1 and "Mango" in week 2, so it has the same name and a new value. Data type, what kind of value: "Biscuit" is text, 3 is a whole number, 12.5 is a decimal, True is true/false, and 2026-09-14 is a date. Data structure, values grouped together: one pet's record holds name Mango, age 1, weight 4.2, adopted False, and arrived 2026-10-02, and the whole pets.csv file holds one record for every pet.](images/m0-name-tag-group.svg)

## Before you read

In the reading, you'll focus on an animal shelter. An **animal shelter** is a place that cares for pets until a new family adopts them, or takes them home. It keeps a record for every pet: its name, age, weight, whether it has been adopted, and the day it arrived.

Here's an answer from a new volunteer: "A pet's weight, like `12.5`, and its tag number, like `00417`, are both made of digits. So the computer should store both as numbers." Something is off about it. What? See if the reading agrees with you.

## ⭐ Read

As you read, look for:

1. Why `=` in `pet_of_the_week = "Biscuit"` means "store," not "is equal to."
2. What happens to the tag number `00417` if the computer stores it as a whole number.
3. Why one line of `pets.csv` is a data structure, not a data type.

**[Start the reading: Name It, Tag It, Group It →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/dev-environment/reading-2-whatkindofdata/)** (about 21 minutes)

## Optional reading (Side Quest)

Want to go further? This reading is optional. You don't need it for the checkpoint, but you can submit it for credit, the same way as a required reading.

**[Start the optional reading: What Shape Is This Data? Structured and Unstructured Data →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/structured_unstructured/)** (about 21 minutes)

## Main takeaways

### Summary

* **A variable is a labeled box.** The label stays the same, and the value inside can change. `pet_of_the_week` held `"Biscuit"`, then `"Mango"`.
* **A data type says what kind of value something is:** text, whole number, decimal, true/false, or date. If you'd never do math with it, treat it as text, even when it's made of digits.
* **A data structure groups values together.** One pet's row is a record. The whole `pets.csv` file, with one record per pet, is a bigger data structure.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "It's made of digits, so it's a number." | A tag number, ZIP code, or phone number is a label. Stored as a whole number, tag `00417` becomes `417`, which is a different pet's tag. Store it as text. |
| "`=` means the two sides are equal." | In code, `=` stores a value in a variable. `pet_of_the_week = "Biscuit"` puts `"Biscuit"` in the box. |
| "A variable holds every value it ever had." | It holds only its newest value. After `"Mango"` is stored, `"Biscuit"` is gone. |
| "Data type and data structure mean the same thing." | A data type describes one value, like `4.2`, a decimal. A data structure groups many values, like Mango's whole row of five values. |
| "If it's in a spreadsheet, it's structured data." | A spreadsheet is a file of rows and columns, like one in Excel or Google Sheets. Structured means the same, clear columns for every row, like `pets.csv`. A spreadsheet where each cell holds a long note about a pet is not well structured. |

### How this connects

* **Next reading:** You'll learn to save a snapshot of your work each time you finish a change, so you have a history of every step. You'll also send a copy of that history to a website, so other people can see it.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll look at a real dataset (a set of data, often one table or file) you've never seen. For each column you look at, you'll decide what kind of data it holds and what it really means.

## Quick check

**1.** A file has a column called `student_id`, with values like `00182` and `01327`. What data type should it be, and why?

<details>
<summary>Answer</summary>

Text. A student ID is a label, not an amount. Nobody adds or averages IDs. Stored as a whole number, `00182` would lose its first zeros and turn into `182`.

</details>

**2.** A classmate says, "The line `Mango,1,4.2,False,2026-10-02` is a data type." What's wrong?

<details>
<summary>Answer</summary>

That line is a data structure: one pet's record. It groups five values together. Each value inside it has its own data type: text, whole number, decimal, true/false, and date.

</details>

---

**Next:** [Quest 0.3 — Save the Story of Your Work: Git and Version Control (Days 2–3)](quest-03-git.md)
