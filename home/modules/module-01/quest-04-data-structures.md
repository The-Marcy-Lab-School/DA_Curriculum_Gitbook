# Quest 1.4 — Pick the Right Container: Lists, Tuples, Sets, and Dictionaries (Day 7)

**Total time:** about 40 minutes

**Building blocks:** Decide and repeat · Organize steps · **Hold data** · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Different jobs need different containers. For example, think about a kitchen. Soup goes in a pot. Eggs go in a carton. Spices go in jars with labels. You find the cumin by reading the labels, not by opening every jar.

Python works the same way. It has four main containers for holding many values. Each one follows its own rules:

* Does it keep the values in order?
* Can it change after you make it?
* Can it hold the same value twice?
* Can you find a value by a label?

In this reading, you'll learn how to:

* tell a list, a tuple, a dictionary, and a set apart
* add to a list, and find a value in a dictionary by its label
* pick the container whose rules fit the job

**Main takeaway:** No container is best for every job. Name the rule the job needs, then pick the container that follows it.

**Why it matters at work:** Most data you'll handle is a list of records, and each record is a dictionary. The wrong container causes quiet bugs, like one customer using a one-time coupon twice.

## Learning goals

Check off each goal once you can do it.

- [ ] I can say how a list, a tuple, a dictionary, and a set differ in order, change, and repeats.
- [ ] I can read, add, and replace values in a list and in a dictionary.
- [ ] I can pick a container for a job and explain my choice with the rule that decides it.

**Skills:** Data Structures & Algorithms

## Quick recall

* Recall that a **list** keeps several values in order, inside square brackets, like `[98, 165, 122]`. A `for` loop visits each item once. You looped over a list of movie lengths in [Trace the Path](quest-01-control-flow.md).
* Recall that you can read a list item by its position: `bookings[3]` is the *fourth* item, because Python starts counting positions at 0. You did this in [When the Crowd Grows](quest-03-big-o-intuition.md).
* Recall that `"QX7RT2" in bookings` checks a list one item at a time, so its work grows with the list. That's O(n). A **lookup** goes straight to one item, like a coat-check ticket, so its work stays the same. That's O(1). You saw both in [When the Crowd Grows](quest-03-big-o-intuition.md). This reading shows the container that lets you look up a value by a label.

## Words to know

### What holds many values?: Data structures

A **container** holds many values under one name. Its formal name is a **data structure**. Each kind has its own rules about order, change, and repeats.

| Word | What it means |
| --- | --- |
| **Data structure** | A container that holds many values under one name, with rules about order, repeats, and change. |
| **Item** | One value inside a container. |
| **Ordered** | The items stay in the order you put them in, so each one has a position. |
| **Position (index)** | An item's place in an ordered container. Python counts positions from 0. |
| **Repeat (duplicate)** | The same value showing up more than once. |
| **Mutable** | Can be changed after it's made. Lists, dictionaries, and sets are mutable. |
| **Immutable** | Can't be changed after it's made. Tuples, strings, and numbers are immutable. |
| **Nested** | One container inside another. Most real data is a list of dictionaries, one dictionary per record. |

### The four containers

| Container | Written with | Can it change? | Repeats allowed? | How you find a value |
| --- | --- | --- | --- | --- |
| **List** | Square brackets `[ ]` | Yes | Yes | By position: `stops[0]` |
| **Tuple** | Parentheses `( )` | No | Yes | By position: `order[1]` |
| **Dictionary (dict)** | Curly braces with pairs `{key: value}` | Yes | Keys: no. Values: yes. | By key: `drivers["D-5521"]` |
| **Set** | Curly braces `{ }`, or `set()` when empty | Yes, by adding values | No | Ask if it's there: `"Sam" in used` |

Lists and tuples keep their order. A set has no fixed order. A dictionary keeps its pairs in the order you added them, but you find a value by its key, not its position.

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

**Code walkthrough:**

1. `stops` is a list of a driver's stops. The stops come in order, and the list can change.
2. `stops.append("Oak Rd")` adds `"Oak Rd"` to the end of the list. `.append()` is a **method**: a function that belongs to a value, called with a dot.
3. `order` is a tuple: a finished order's code and drop-off time. It can never change, so the record stays correct.
4. `drivers` is a dictionary. The key `"D-5520"` is an order code, and the value `"Noor"` is the driver's name.
5. `drivers["D-5521"] = "Sam"` adds a new pair. If the key already existed, this line would replace its value instead.
6. `set()` makes an empty set, and `used.add("Noor")` puts a customer's name in it. Adding `"Noor"` a second time would change nothing.

{% hint style="info" %}
**`{}` is an empty dictionary, not an empty set.** To make an empty set, write `set()`.
{% endhint %}

### Working inside a container: Keys, values, and errors

| Word | What it means |
| --- | --- |
| **Key** | The label you look a value up by, in a dictionary. Each key appears only once. Keys must be immutable, like strings, numbers, or tuples. A list can't be a key. |
| **Value** | The data stored under a key. |
| **Key/value pair** | One key and its value, stored together. |
| **Lookup** | Going straight to a value by its key, instead of checking items one by one. A dictionary lookup is O(1): about the same work with 2 orders or 20,000. |
| **Method** | A function that belongs to a value. You call it with a dot and parentheses, like `stops.append("Oak Rd")` or `used.add("Noor")`. |
| **Unpacking** | Taking a tuple apart into separate variables. In `for code, time in finished:`, the first item goes into `code` and the second into `time`. |
| **Built-in function** | A function that comes with Python, like `len()`, `set()`, and `type()`. `type()` tells you what kind of value something is. |
| **`TypeError`** | The error Python raises when a value can't do what you asked. For example, trying to change an item in a tuple raises a `TypeError`. |

## Before you read

In the reading, you'll focus on a food delivery app. Every night it tracks four kinds of data:

* a driver's list of stops
* finished orders that must never change
* which driver has each order
* which customers already used a first-order coupon

Think about: which of these should be able to change during the night, and which should never change? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. What Python does when code tries to change an item in a tuple, and why that error is helpful.
2. Why keeping order codes in one list and driver names in a second list is risky, and how a dictionary fixes it.
3. Why `{}` can't make an empty set.

**[Start the reading: Pick the Right Container →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/python-data-structures/reading1-pickrightcontainer/)** (about 24 minutes)

## Main takeaways

### Summary

* **A list changes, and a tuple doesn't.** Both keep their order. Use a list for data that grows or changes, like a shopping cart. Use a tuple for a record that must stay fixed, like a posted rating. Changing a tuple raises a `TypeError`, and that error protects the record.
* **A dictionary finds a value by its key.** Each key appears once and maps to one value. A lookup takes about one step, and each key stays with its value, so pairs can't get mixed up.
* **A set keeps each value once.** Use it when you only need to know "is this value here?" Make an empty set with `set()`, because `{}` makes an empty dictionary.

In an interview, name the rule that decides your choice: order, change, lookup by key, or no repeats. This decision tree asks those questions in order:

![A decision tree using the food delivery app. First question: do you find each value by a label (a key)? If yes, use a dictionary, like drivers["D-5521"], which gives Sam. If no, second question: does each value only need to be there once? If yes, use a set, like used.add("Noor") for customers who used a coupon. If no, third question: must the data never change? If yes, use a tuple, like the finished order ("D-5520", "7:42 PM"). If no, use a list, like a driver's stops with stops.append("Oak Rd"). A note says a list is the default: it keeps order, allows repeats, and can change.](images/m1b-which-container.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "A list works for everything." | A list allows repeats and searches item by item. A set blocks repeats, and a dictionary finds a value in one step. |
| "`{}` makes an empty set." | It makes an empty dictionary. Use `set()`. |
| "Two lists matched by position work like a dictionary." | Delete an item from one list and forget the other, and every pair after it is mismatched, with no error. |
| "A tuple is just a list with round brackets." | A tuple can't change after it's made. That's the point: it protects records that must stay fixed. |
| "Any value can be a dictionary key." | Keys must be immutable. Strings, numbers, and tuples work. A list doesn't. |

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
