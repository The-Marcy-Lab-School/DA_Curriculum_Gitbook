# Quest 1.3 — When the Crowd Grows: How Code Speed Scales (Day 6)

**Total time:** about 35 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · Load, save, and protect · **Check your work** ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Some ways of searching get slower as the pile grows. For example, a teacher looks for one student's paper in a pile. She checks one paper at a time. With 10 papers, it takes a few seconds. With 1,000 papers, it could take a long time. But if the papers are filed in folders by name, she goes straight to the right folder. The pile size barely matters.

In this reading, you'll learn how to:

* count the steps a search takes in the worst case
* describe how that count grows as the data grows
* tell a search that checks every item apart from a lookup that jumps straight to one

**Main takeaway:** Ask one question about your code: "What happens to the amount of work as the data grows?" Big-O is the language for the answer.

**Why it matters at work:** Code that feels instant on a test file of 50 rows can be very slow on 5 million rows. Analysts who think about growth early pick an approach that still works on the full data.

## Learning goals

Check off each goal once you can do it.

- [ ] I can count the worst-case checks in a linear search, and say how they change when the list doubles.
- [ ] I can explain O(n) and O(1) in plain words.
- [ ] I can explain why a fast test on a few items doesn't prove the code stays fast on many.

**Skills:** Algorithmic Complexity (Big-O)

## Quick recall

* Recall that you counted a loop's passes one at a time. A loop inside a loop runs its inner body (outer passes × inner passes) times. You did this in [Trace the Path](quest-01-control-flow.md). Counting passes is how you'll measure work in this reading.
* Recall that `return` ends a function right away, even inside a loop, from [Build It Once, Use It Again](quest-02-functions-scope.md). The search in this reading uses that: it returns as soon as it finds a match.

## Words to know

### How much work?: Algorithms and input size

An **algorithm** is a list of steps that solves a problem. For example, "check each booking in order until one matches" is an algorithm. To compare two algorithms, count their steps, not seconds.

| Word | What it means | Units |
| --- | --- | --- |
| **Input size (n)** | How many items an algorithm works through, like the number of bookings. Big-O calls it `n`. | Items (here, bookings) |
| **Check** (or **step**) | One small piece of work, like comparing one booking to the code you want. | Checks |
| **Worst case** | The situation that takes the most work. For a search, the item is last, or not there at all. | Checks |
| **Best case** | The situation that takes the least work. For a search, the item is first, so it takes 1 check. | Checks |
| **Runtime** | How long one run takes on one computer. It changes from laptop to laptop, so Big-O counts steps instead. | Seconds |

### Two ways to find an item: Linear search and lookup

| Word | What it means |
| --- | --- |
| **Linear search** (or **linear scan**) | Check items one at a time, in order, until you find the target or run out of items. *Linear* means "in a line." |
| **`in`** | `"QX7RT2" in bookings` gives `True` if the list holds that item and `False` if it doesn't. On a list, `in` is a linear search: it checks from the start, one item at a time. |
| **`len()`** | A function that gives how many items a list holds. `len(bookings)` gives the input size, `n`. |
| **Lookup** | Go straight to one item by its position or label, like a coat-check worker walking to hook 42. |
| **Index** | An item's position number in a list. Python starts counting at 0, so `bookings[0]` is the first item and `bookings[3]` is the fourth. |

![Two panels side by side, with the same 4 bookings in positions 0 to 3: LM2B8K, RT9PW4, BB4HN1, and QX7RT2. Left, linear search: it checks positions 0, 1, 2, and 3 in order, so finding QX7RT2 at the end takes 4 checks. With 8 bookings, it takes 8 checks. This is O(n), the work grows with n. Right, lookup: bookings[3] jumps straight to position 3 in 1 step. With 200,000 bookings, it's still about 1 step. This is O(1), the work stays about the same.](images/m1a-search-vs-lookup.svg)

### How does the work grow?: Big-O

**Grow** here means "get bigger as the data gets bigger." Big-O describes the *shape* of that growth, not the exact number of seconds.

| Word | What it means |
| --- | --- |
| **Big-O** | A way to describe how an algorithm's work grows as its input size grows. |
| **O(n)**, said "O of n" | The work grows with the number of items. Double the items, and the worst case doubles. A linear search is O(n). |
| **O(1)**, said "O of 1" | The work stays about the same, however many items there are. A lookup by position is O(1). |
| **Scale** | How an algorithm behaves as its input grows from small to very large. Code that stays fast as the data grows **scales well**. |

{% hint style="info" %}
**O(1) doesn't mean zero time, and O(n) doesn't mean slow.** A linear search over 5 items finishes almost at once. Both labels describe how the work *grows*, not how long one run takes.
{% endhint %}

## Before you read

In the reading, you'll focus on an airport check-in screen. It finds your booking from a six-letter code. With 200 bookings, any search feels instant.

Think about: if the airline grows to 200,000 bookings, how many might the screen have to check to find yours? Does it matter where your booking sits in the list? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Where a booking has to sit for a linear search to do the most work.
2. What happens to the worst-case checks when the list doubles from 4 bookings to 8.
3. Why a lookup like `bookings[3]` does about the same work for 4 bookings or 200,000.

**[Start the reading: When the Crowd Grows →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/big-o-intuition/reading-1-whenthecrowdgrows/)** (about 23 minutes)

## Main takeaways

### Summary

* **Big-O is about growth, not seconds.** It answers one question: "As the input size grows, what happens to the amount of work?"
* **A linear search is O(n).** In the worst case, it checks all `n` items. So double the items means double the checks. Using `in` on a list is a linear search too.
* **A lookup is O(1).** It jumps straight to the item. The work stays about the same as the data grows. A fast test on a few items can't show you which kind you have.

![Two bar charts side by side with the same axes. The x-axis is the number of bookings: 25,000, 50,000, 100,000, and 200,000. The y-axis is worst-case steps, from 0 to 200,000. Left, linear search, O(n): the bars rise to 25,000, 50,000, 100,000, and 200,000 steps, doubling each time the bookings double. Right, lookup by code, O(1): every bar stays at about 1 step, too small to see.](images/m1a-growth-compare.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Big-O tells me how many seconds my code takes." | It tells you how the work *grows* as the data grows. Seconds change from computer to computer. |
| "O(1) means it takes no time." | It means the work stays about the same as the data grows. It still takes a little time. |
| "O(n) means the code is slow." | A small O(n) search can finish almost at once. The problem shows up when `n` gets very large. |
| "It was fast on 50 items, so it will be fast on 5 million." | A small test doesn't show growth. An O(n) search on 5 million items does up to 5 million checks. |
| "`in` is one step, because it's one word." | On a list, `in` checks items one at a time from the start. Its work grows with the list. |

### How this connects

* **Next reading:** You'll compare the containers Python offers for holding many values. One of them files each item under a label, like a coat-check ticket. So finding an item by its label stays fast as the data grows.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll explain how the work in your code grows as the data grows. You'll also choose a way to find items that stays fast on large data.

## Quick check

**1.** A store's list holds 1,000 product names. A linear search looks for a product that isn't on the list. How many checks does it make? What if the list grows to 5,000 names?

<details>
<summary>Answer</summary>

1,000 checks, then 5,000 checks. The product isn't there, so this is the worst case: the search checks every item. The list grew 5 times, so the work grew 5 times. That's O(n).

</details>

**2.** A teammate says, "My search took almost no time on five items, so we don't need to think about speed." What's missing from that reasoning?

<details>
<summary>Answer</summary>

Five items only show how the search works on a tiny input. They don't show how the work grows as the data gets much bigger. Ask, "What happens as the input gets bigger?"

</details>

---

**Next:** [Quest 1.4 — Pick the Right Container: Lists, Tuples, Sets, and Dictionaries (Day 7)](quest-04-data-structures.md)
