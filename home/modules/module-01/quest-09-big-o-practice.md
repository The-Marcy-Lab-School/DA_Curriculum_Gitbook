# Quest 1.9 — Lookups Matter: Search Speed in Practice (Days 16–17)

**Total time:** About 35 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · Load, save, and protect · **Check your work** ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

How you look for something matters more as the pile grows. For example, you need one word in a book. You can turn the pages one by one from the start. Or you can use the index at the back, which sends you straight to the right page. In a 10-page booklet, turning pages is fine. In a 900-page book, the index saves a lot of time.

**Main takeaway:** To find items fast in big data, build a dictionary once, then look items up by key. A **dictionary lookup** finds a value straight from its key, in about one step at any size. A **linear search** checks items one at a time, so with 400K saved callers, one call can mean 400K checks. (K means thousand and M means million, so 400K is 400,000.)

**Why it matters at work:** Analysts choose how to store records so that finding one stays fast as the data grows. For example, they use dictionary lookups to:

* find a caller's name from their phone number
* match each order to its customer by customer ID
* check whether a product code is already saved

If they search a list instead, code that felt instant on 20 rows can make people wait several seconds on 400K.

## Learning goals

After this reading, you should be able to say:

* I can explain in plain words why a linear search is O(n) and a dictionary lookup is O(1) on average.
* I can build a dictionary from a list with a loop, and look up a key with `.get()` so a missing key gives `None` instead of an error.
* I can decide when a list search is fine and when building a dictionary pays off (is worth the extra work).

**Skills:** Algorithmic Complexity (Big-O) · Data Structures & Algorithms

## Quick recall

* Recall that a linear search checks items one at a time, and that Big-O describes how the work grows as the input grows, from [When the Crowd Grows](quest-03-big-o-intuition.md). In its interactive reading, when a list of 300 bookings (saved seats on flights) doubles to 600, the worst case doubles from 300 checks to 600.
* Recall that a dictionary stores each value under a key, from [Pick the Right Container](quest-04-data-structures.md). In its interactive reading, `drivers["D-5521"]` gives the value stored under the key `"D-5521"`, and `drivers["D-5522"] = "Ari"` adds a new pair.
* Recall that a **method** is a function that belongs to an object, called with a dot and parentheses, from [Meet the Objects](quest-08-oop.md). In this reading, `.get()` is a method that every dictionary has.

## Words to know

### How do you find one item?: Linear search and dictionary lookup

The examples come from the reading's short list of 3 saved callers: Ana Ruiz, Sam Lee, and Kim Park.

| Word | What it means | Example |
| --- | --- | --- |
| **Record** | One saved entry with a few values that belong together, like a phone number and a name. In the reading, each record is a small dictionary. | `{"phone": "555-0113", "name": "Kim Park"}` |
| **Linear search** | Checking items one at a time, in order, until one matches or none are left. | To find `"555-0113"`, check Ana, then Sam, then Kim: 3 checks. |
| **Dictionary lookup** | Finding a value straight from its key. | `callers_by_phone.get("555-0113")` gives `"Kim Park"`. |
| **`.get(key)`** | A dictionary method that looks up a key. It returns the value, or `None` when the key is missing. | `callers_by_phone.get("555-0199")` gives `None`. |
| **`None`** | Python's value for "nothing here." Python code checks for it with `is`. | `if name is None:` then print `New caller` |
| **`KeyError`** | The error Python raises when you use square brackets with a key that isn't in the dictionary. | `callers_by_phone["555-0199"]` |

Two ideas here build on earlier pages:

* The keys are phone numbers, like `"555-0113"`. Recall from [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md) that a phone number is a label, not an amount. So it's stored as text, in quotes.
* You caught a `KeyError` with `try` and `except KeyError:` in [Validate, Catch, Keep Going](quest-06-validation-errors.md). `.get()` is another way to handle a missing key, with no error at all.

### How does the work grow?: Big-O and complexity

Big-O counts **steps** (checks), not seconds on a clock. In this table, the input size is counted in callers, and the work is counted in checks or steps.

| Word | What it means | Example with the help line |
| --- | --- | --- |
| **Input size (n)** | How many items the code has to work through. For the help line, n is the number of saved callers. | The short list: n = **3 callers**. The full help line: n = **400K callers**. |
| **Worst case** | The input that makes code do the most work. For a linear search, the item is last or not there at all, so every item gets checked. | `"555-0199"` isn't saved, so all 3 callers get checked = **3 checks** |
| **O(n)** | The work grows in step with the input size. Double n, and the worst case doubles. A linear search is O(n). | 20 callers: up to **20 checks**. 400K callers: up to **400K checks**. |
| **O(1) average-case** | A typical lookup takes about one step, no matter how big n gets. A rare one can take a little longer. A dictionary lookup is O(1) on average. | `.get("555-0113")` takes about **1 step** for 3 callers or 400K. |
| **Complexity** | How much work code does as its input grows, written in Big-O, such as O(n) or O(1). | Linear search: O(n). Dictionary lookup: O(1). |
| **Scale** | How a cost changes as the data grows. Two searches can tie on 10 items and be far apart on 10 million. | At 400K callers: up to 400K checks, or about 1 step. |

## Before you read

In the reading, you'll focus on a help line: a phone number people call to get help. When someone calls, the screen shows the caller's name. The program finds it by searching a list of saved callers for the phone number. With 20 saved callers, the name appeared at once. With 400K, people wait several seconds.

Think about: the code didn't change, so why did it slow down? What would you change? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. How many records the search checks when the phone number is last, or not saved at all.
2. What it costs to build the dictionary, and how often you pay that cost.
3. What square brackets do with a missing key, and what `.get()` does instead.

**[Start the reading: Lookups Matter →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/python-data-structures/reading-2-lookupsmatter/)** (about 23 minutes)

## Optional reading (Side Quest)

Want to go further? This reading is optional. You don't need it for the checkpoint, but you can submit it for credit, the same way as a required reading.

**[Start the optional reading: Straight to the Slot: Hash Maps →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/hash-maps/reading-1-straight-to-the-slot/)** (about 22 minutes)

## Main takeaways

### Summary

* **A linear search is O(n).** In the worst case, it checks every record. With 400K saved callers, one call can mean 400K checks.
* **Build the dictionary once, then look up many times.** Building `callers_by_phone` with a loop visits every record once: O(n), paid one time. Each lookup after that is O(1) on average, about one step at any size.
* **Use `.get()` when a key might be missing.** Square brackets raise a `KeyError` and stop the program. `.get()` returns `None`, so your code can treat the number as a new caller.

![Side by side. Left, a linear search looks for 555-0199 in three saved callers, Ana Ruiz, Sam Lee, and Kim Park. Each check says no, and it returns None after 3 checks. In the worst case it checks all n records: O(n). Right, a dictionary lookup. Step 1 builds callers_by_phone once with a loop, O(n), one time. Step 2, .get("555-0113"), goes straight to Kim Park in about 1 step at any size: O(1) average-case. At the bottom: with 400K saved callers, one call can mean up to 400K checks with a linear search, or about 1 step with a dictionary lookup.](images/m1c-linear-vs-dict.svg)

A list search is still fine when the list is tiny or you search only once. Then building a dictionary costs about as much as the search it replaces. For example, one search of 12 test callers takes up to 12 checks. Building the dictionary takes 12 steps, plus 1 step for the lookup. A dictionary pays off when you search many times, or when the data keeps growing.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "A dictionary is faster at every size, so I should always build one." | For one search of 12 callers, the list takes up to 12 checks. The dictionary takes 12 steps to build, plus 1 to look up. It pays off when you search many times. |
| "My list search beat the dictionary on 3 items, so it has better Big-O." | Big-O describes growth, not one small race. At 400K callers, the list can take 400K checks, and the lookup about 1 step. |
| "O(1) means exactly one step, every time." | It means about the same work at any size, on average: about 1 step for 3 callers or 400K. A rare lookup can take a little longer. |
| "`callers_by_phone["555-0199"]` gives `None` when the number isn't saved." | Square brackets raise `KeyError: '555-0199'`. Only `.get()` returns `None`. |
| "A linear search always checks every item." | It stops at the first match. Finding `"555-0142"`, the first record, takes 1 check. Only the worst case checks every item. |

### How this connects

* **Next reading:** Fast code can still give the wrong answer. You'll learn to work out the right answer by hand first, then compare it with what the code prints. That catches mistakes that never show an error message.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll choose how to store and search your program's records. Then you'll explain, in plain words, the tradeoff between searching a list and looking up a key. A **tradeoff** is a choice where you gain one thing but give up another.

## Quick check

**1.** A list holds 50,000 product codes. A program checks whether a code is in that list 10,000 times a day. Should it keep searching the list, or build a dictionary first? Why?

<details>
<summary>Answer</summary>

Build a dictionary (or a set) first. With the list, each check can take up to 50,000 comparisons. Done 10,000 times a day, that's up to 50,000 × 10,000 = 500M comparisons. Building the dictionary costs O(n) once: 50,000 steps. After that, the 10,000 checks take about 10,000 steps.

</details>

**2.** What does this code print?

```python
prices = {"tea": 3, "coffee": 4}
print(prices.get("juice"))
print(prices["juice"])
```

<details>
<summary>Answer</summary>

It prints `None`. Then the program stops with `KeyError: 'juice'`. `.get()` returns `None` for a missing key, but square brackets raise an error.

</details>

---

**Next:** [Quest 1.10 — Looks Right. Is It? Debugging (Days 18–19)](quest-10-debugging.md)
