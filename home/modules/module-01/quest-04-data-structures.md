# Quest 1.4 — Pick the Right Container: Lists, Tuples, Sets, and Dictionaries (Day 7)

**Total time:** About 40 minutes

**Building blocks:** Decide and repeat · Organize steps · **Hold data** · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* In Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), one pet's row in `pets.csv` was a small **data structure** called a **record**. A data structure groups several values as one unit, and this reading shows Python's four main ones.
* Your `for` loop in [Trace the Path](quest-01-control-flow.md) visited each movie length in a **list** once. A list keeps values in order, inside square brackets, like `[98, 165, 122]`.
* In [When the Crowd Grows](quest-03-big-o-intuition.md), `"QX7RT2" in bookings` checked one item at a time, so its work grew: O(n). A **lookup** like `bookings[3]`, counting from 0, went straight to one item, like a coat-check ticket: O(1). This reading shows a container that looks up a value by a label.

## Introduction

Different jobs need different containers. For example, think about a kitchen. Soup goes in a pot. Eggs go in a carton. Spices go in jars with labels. You find the cumin by reading the labels, not by opening every jar.

Python works the same way. It has four main containers for holding many values. Each one follows its own rules:

* Does it keep the values in order?
* Can it change after you make it?
* Can it hold the same value twice?
* Can you find a value by a label?

**Main takeaway:** Pick the data structure whose rules fit the job. A **data structure** (or container) holds many values under one name, with rules about order, change, and repeats. For example, a set fits the coupon job, because it keeps each customer's name only once.

**Why it matters at work:** Analysts choose a container every time they hold data in code. For example, they use containers to:

* keep a list of **records**, one dictionary per order (a record is the data about one thing)
* look up a customer's details by their customer ID
* keep track of which customers already used a one-time coupon

The wrong container causes quiet bugs (mistakes in code that show no error), like one customer using a one-time coupon twice.

## Learning goals

After this reading, you should be able to say:

* I can say how a list, a tuple, a dictionary, and a set differ in order, change, and repeats.
* I can read, add, and replace values in a list and in a dictionary.
* I can pick a container for a job and explain my choice with the rule that decides it.

**Skills:** Data Structures & Algorithms

## Words to know

### What holds many values?: Data structures

A **container** holds many values under one name. Its formal name is a **data structure**. Each kind has its own rules about order, change, and repeats.

The examples come from the reading's food delivery app.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Data structure** | A container that holds many values under one name, with rules about order, repeats, and change. | `stops`, a driver's list of streets |
| **Item** | One value inside a container. | `"Elm St"` in `stops` |
| **Ordered** | The items stay in the order you put them in, so each one has a position. | `stops` keeps `"Elm St"` before `"Pine Ave"`. |
| **Position (index)** | An item's place in an ordered container. Python counts positions from 0. | `stops[0]` is `"Elm St"`. |
| **Repeat (duplicate)** | The same value showing up more than once. | `"Noor"` added to the coupon list twice |
| **Mutable** | Can be changed after it's made. Lists, dictionaries, and sets are mutable. | `stops.append("Oak Rd")` changes `stops`. |
| **Immutable** | Can't be changed after it's made. Tuples, strings, and numbers are immutable. | `order[1] = "7:50 PM"` stops with an error. |
| **Nested** | One container inside another. Most real data is a list of dictionaries, one dictionary per record. | `[("D-5520", "7:42 PM"), ("D-5521", "7:58 PM")]`: a list of tuples |

### The four containers

| Container | Written with | Can it change? | Repeats allowed? | How you find a value |
| --- | --- | --- | --- | --- |
| **List** | Square brackets `[ ]` | Yes | Yes | By position: `stops[0]` |
| **Tuple** | Parentheses `( )` | No | Yes | By position: `order[1]` |
| **Dictionary (dict)** | Curly braces with pairs `{key: value}` | Yes | Keys: no. Values: yes. | By key: `drivers["D-5521"]` |
| **Set** | Curly braces `{ }`, or `set()` when empty | Yes, by adding values | No | Ask if it's there: `"Sam" in used` |

Lists and tuples keep their order. A set has no fixed order. A dictionary keeps its pairs in the order you added them, but you find a value by its key, not its position.

You already know lists. Here is how each new container acts differently from a list:

| New container | With a list | With the new container |
| --- | --- | --- |
| **Tuple: can't change** | `stops[0] = "Main St"` replaces the first stop. | `order[1] = "7:50 PM"` stops with a `TypeError`. |
| **Dictionary: find by key** | `stops[1]` finds `"Pine Ave"` by its position. | `drivers["D-5521"]` finds `"Sam"` by its key. |
| **Set: no repeats** | Add `"Noor"` twice, and the list holds 2 items. | Add `"Noor"` twice, and the set holds 1 item. |

For example, here are all four containers from the reading's food delivery app:

```python
stops = ["Elm St", "Pine Ave"]    # list
stops.append("Oak Rd")            # add to the end
order = ("D-5520", "7:42 PM")     # tuple
drivers = {"D-5520": "Noor"}      # dict
drivers["D-5521"] = "Sam"         # add a pair
used = set()                      # empty set
used.add("Noor")
```

<details>
<summary>Expand to walk through the code</summary>

1. `stops` is a list of a driver's stops: the streets where the driver drops off food. The stops come in order, and the list can change.
2. `stops.append("Oak Rd")` adds `"Oak Rd"` to the end of the list. `.append()` is a **method**: a function that belongs to a value, called with a dot.
3. `order` is a tuple: a finished order's code and drop-off time (when the food was delivered). It can never change, so the record stays correct.
4. `drivers` is a dictionary. The key `"D-5520"` is an order code, and the value `"Noor"` is the driver's name.
5. `drivers["D-5521"] = "Sam"` adds a new pair. If the key already existed, this line would replace its value instead.
6. `set()` makes an empty set, and `used.add("Noor")` puts a customer's name in it. Adding `"Noor"` a second time would change nothing.

</details>

{% hint style="info" %}
**`{}` is an empty dictionary, not an empty set.** To make an empty set, write `set()`.
{% endhint %}

### Working inside a container: Keys, values, and errors

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Key** | The label you look a value up by, in a dictionary. Each key appears only once. Keys must be immutable, like strings, numbers, or tuples. A list can't be a key. | `"D-5520"` in `drivers` |
| **Value** | The data stored under a key. | `"Noor"`, stored under `"D-5520"` |
| **Key/value pair** | One key and its value, stored together. | `"D-5520": "Noor"` |
| **Lookup** | Going straight to a value by its key, instead of checking items one by one. A dictionary lookup is O(1): about the same work with 2 orders or 20,000. | `drivers["D-5521"]` gives `"Sam"`. |
| **Method** | A function that belongs to a value. You call it with a dot and parentheses. | `stops.append("Oak Rd")` or `used.add("Noor")` |
| **Unpacking** | Taking a tuple apart into separate variables. | In `for code, time in finished:`, `code` gets `"D-5520"` and `time` gets `"7:42 PM"`. |
| **Built-in function** | A function that comes with Python, like `len()`, `set()`, and `type()`. `type()` tells you what kind of value something is. | `type({})` gives `<class 'dict'>`. |
| **`TypeError`** | The error Python raises when a value can't do what you asked. | Changing an item in a tuple: `order[1] = "7:50 PM"` |

A dictionary builds on two ideas from [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md):

* A **key** works like an ID: it labels one thing. The order code `"D-5520"` is an ID, so it's stored as text.
* One dictionary can hold one **record**. Each key works like a column name. For example, `{"name": "Mango", "age": 1}` holds part of one pet's record.

## Before you read

In the reading, you'll focus on a food delivery app. Every night it tracks four kinds of data:

* a driver's list of stops
* finished orders that must never change
* which driver has each order
* which customers already used a first-order coupon

Think about: which of these should be able to change during the night, and which should never change? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

As you read, look for:

1. What Python does when code tries to change an item in a tuple, and why that error is helpful.
2. Why keeping order codes in one list and driver names in a second list is risky, and how a dictionary fixes it.
3. Why `{}` can't make an empty set.

**[Start the reading: Pick the Right Container →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/python-data-structures/reading1-pickrightcontainer/)** (about 24 minutes)

## Optional reading (Side Quest)

Want to go further? These readings are optional. You don't need them for the checkpoint, but you can submit them for credit, the same way as a required reading.

**[Start the optional reading: Link by Link: Linked Lists →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/linked-lists/reading-1-link-by-link/)** (about 24 minutes)

**[Start the optional reading: The Deepest Branch: Binary Trees →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/trees/reading-1-the-deepest-branch/)** (about 23 minutes)

## Main takeaways

### Summary

* **A list changes, and a tuple doesn't.** Both keep their order. Use a list for data that grows or changes, like a shopping cart. Use a tuple for a record that must stay fixed, like a posted rating (a review score that is already shared online). Changing a tuple raises a `TypeError`, and that error protects the record.
* **A dictionary finds a value by its key.** Each key appears once and maps to one value. A lookup takes about one step, and each key stays with its value, so pairs can't get mixed up.
* **A set keeps each value once.** Use it when you only need to know "is this value here?" Make an empty set with `set()`, because `{}` makes an empty dictionary.

In an interview, name the rule that decides your choice: order, change, lookup by key, or no repeats. The decision tree below asks those questions in order. Start at the top question, and follow each yes or no.

![A decision tree using the food delivery app. First question: do you find each value by a label (a key)? If yes, use a dictionary, like drivers["D-5521"], which gives Sam. If no, second question: does each value only need to be there once? If yes, use a set, like used.add("Noor") for customers who used a coupon. If no, third question: must the data never change? If yes, use a tuple, like the finished order ("D-5520", "7:42 PM"). If no, use a list, like a driver's stops with stops.append("Oak Rd"). A note says a list is the default: it keeps order, allows repeats, and can change.](images/m1b-which-container.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I can just use a list for everything." | A list allows repeats. Add `"Noor"` to a coupon list twice, and the list holds her 2 times. A set holds her once. |
| "`{}` makes an empty set." | `type({})` gives `<class 'dict'>`: it's an empty dictionary. Use `set()`. |
| "Two lists matched by position work just like a dictionary." | Codes `["D-5520", "D-5521"]` match names `["Noor", "Sam"]`. Delete `"D-5520"` but not `"Noor"`, and `"D-5521"` now lines up with Noor, not Sam. No error shows up. |
| "A tuple is just a list with round brackets." | A tuple can't change. `order[1] = "7:50 PM"` raises a `TypeError`, so the finished order keeps its `"7:42 PM"` time. |
| "Any value can be a dictionary key." | Keys must be immutable. The string `"D-5520"` works as a key. The list `["D-5520"]` doesn't. |

### How this connects

* **Next reading:** Every container you make is gone when the program stops. Next, you'll save a dictionary to a file and load it back in a later run. Then you'll check what changed about the data on the way.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll hold real records in containers you choose, and explain each choice with the rule that decides it.

## Quick check

**1.** A school office needs to find each student's locker number from their student ID. Which container fits best, and why?

<details>
<summary>Answer</summary>

A dictionary. The student ID is the key and the locker number is the value. The office looks up a value by a label, and each ID appears only once.

</details>

**2.** What does this code print?

```python
tags = set()
tags.add("rain")
tags.add("wind")
tags.add("rain")
print(len(tags))
```

<details>
<summary>Answer</summary>

`2`. A set keeps each value once, so adding `"rain"` a second time changes nothing.

</details>

---

**Next:** [Quest 1.5 — Make It Survive: Saving Data to Files (Day 8)](quest-05-serialization.md)
