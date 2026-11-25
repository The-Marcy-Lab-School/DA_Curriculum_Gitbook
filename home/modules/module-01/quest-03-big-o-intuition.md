# Quest 1.3 — When the Crowd Grows: How Code Speed Scales (Day 6)

**Total time:** About 35 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · Load, save, and protect · **Check your work** ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* Counting a loop's passes, as you did in [Trace the Path](quest-01-control-flow.md), is how this reading measures work. A loop inside a loop runs its inner body (outer passes × inner passes) times.
* `return` ends a function right away, even inside a loop, as you saw in [Build It Once, Use It Again](quest-02-functions-scope.md). The search in this reading returns as soon as it finds a match.
* An **ID** labels one thing, like a pet's tag number, as Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md) showed. A booking code like `"QX7RT2"` is an ID too, and this reading searches a list of them.

## Introduction

Some ways of searching get slower as the pile grows. For example, a teacher looks for one student's paper in a pile. She checks one paper at a time. With 10 papers, it takes a few seconds. With 1,000 papers, it could take a long time. But if the papers are filed in folders by name, she goes straight to the right folder. The pile size barely matters.

**Main takeaway:** Before you trust code on big data, ask how its work grows as the data grows. **Big-O** is the way to describe that growth. For example, a search that checks bookings one at a time does up to 4 checks for 4 bookings. For 8 bookings, it does up to 8. A lookup takes about 1 step at either size.

**Why it matters at work:** Analysts think about growth so they pick code that still works on the full data. For example, they use it to:

* choose how to store customer records, so finding one stays fast
* judge whether a script tested on 50 rows will still work on 5 million (5M) rows
* explain in an interview why one approach scales better than another

If you skip this, a search that checked 50 rows in a test may check 5M rows at work: 100K times as much work. (K means thousand and M means million, so 100K is 100,000 and 5M is 5,000,000.)

## Learning goals

After this reading, you should be able to say:

* I can count the worst-case checks in a linear search, and say how they change when the list doubles.
* I can explain O(n) and O(1) in plain words.
* I can explain why a fast test on a few items doesn't prove the code stays fast on many.

**Skills:** Algorithmic Complexity (Big-O)

## Words to know

### How much work?: Algorithms and input size

An **algorithm** is a list of steps that solves a problem. For example, "check each booking in order until one matches" is an algorithm. A **booking** is one person's saved seat on a flight. To compare two algorithms, count their steps, not seconds.

**Units** are what a number counts. The input size is counted in bookings. The work is counted in checks. Runtime is the one exception: it's counted in seconds. The examples use the reading's list of 4 bookings:

`bookings = ["LM2B8K", "RT9PW4", "BB4HN1", "QX7RT2"]`

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Input size (n)** | How many items an algorithm works through, like the number of bookings. Big-O calls it `n`. | `len(bookings)` = **4 bookings** |
| **Check** (or **step**) | One small piece of work, like comparing one booking to the code you want. | Is `"LM2B8K"` equal to `"QX7RT2"`? = **1 check** |
| **Worst case** | The situation that takes the most work. For a search, the item is last, or not there at all. | `"ZZ1AA1"` isn't in the list, so all 4 get checked = **4 checks** |
| **Best case** | The situation that takes the least work. For a search, the item is first. | `"LM2B8K"` is first = **1 check** |
| **Runtime** | How long one run takes on one computer. It changes from laptop to laptop, so Big-O counts steps instead. | An older laptop takes more **seconds**, but it still makes 4 checks. |

### Two ways to find an item: Linear search and lookup

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Linear search** (or **linear scan**) | Check items one at a time, in order, until you find the target or run out of items. *Linear* means "in a line." | To find `"QX7RT2"`, check positions 0, 1, 2, then 3: 4 checks. |
| **`in`** | Gives `True` if the list holds that item and `False` if it doesn't. On a list, `in` is a linear search: it checks from the start, one item at a time. | `"QX7RT2" in bookings` gives `True`. |
| **`len()`** | A function that gives how many items a list holds: the input size, `n`. | `len(bookings)` gives `4`. |
| **Lookup** | Go straight to one item by its position or label. | A coat-check worker walks straight to hook 42. (At a **coat check**, you leave your coat and get a ticket with a hook number.) |
| **Index** | An item's position number in a list. Python starts counting at 0. | `bookings[0]` is the first item, `"LM2B8K"`. `bookings[3]` is the fourth, `"QX7RT2"`. |

In [Trace the Path](quest-01-control-flow.md), `range(n)` also started at 0 and stopped before `n`. So `range(4)` gives 0, 1, 2, and 3: the four positions in a list of four items.

The picture below finds `"QX7RT2"` both ways. Compare the 4 checks on the left with the 1 step on the right.

![Two panels side by side, with the same 4 bookings in positions 0 to 3: LM2B8K, RT9PW4, BB4HN1, and QX7RT2. Left, linear search: it checks positions 0, 1, 2, and 3 in order, so finding QX7RT2 at the end takes 4 checks. With 8 bookings, it takes 8 checks. This is O(n), the work grows with n. Right, lookup: bookings[3] jumps straight to position 3 in 1 step. With 200K bookings, it's still about 1 step. This is O(1), the work stays about the same.](images/m1a-search-vs-lookup.svg)

### How does the work grow?: Big-O

**Grow** here means "get bigger as the data gets bigger." Big-O describes the *shape* of that growth, not the exact number of seconds.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Big-O** | A way to describe how an algorithm's work grows as its input size grows. | A linear search is O(n). A lookup is O(1). |
| **O(n)**, said "O of n" | The work grows with the number of items. Double the items, and the worst case doubles. A linear search is O(n). | 4 bookings: up to 4 checks. 8 bookings: up to 8 checks. |
| **O(1)**, said "O of 1" | The work stays about the same, however many items there are. A lookup by position is O(1). | `bookings[3]` takes about 1 step for 4 bookings or 200K. |
| **Scale** | How an algorithm behaves as its input grows from small to very large. Code that stays fast as the data grows **scales well**. | From 25,000 to 200K bookings, a lookup stays at about 1 step. It scales well. |

{% hint style="info" %}
**O(1) doesn't mean zero time, and O(n) doesn't mean slow.** A linear search over 5 items finishes almost at once. Both labels describe how the work *grows*, not how long one run takes.
{% endhint %}

## Before you read

In the reading, you'll focus on an airport check-in screen: a screen where travelers show they are there for their flight. It finds your booking from a six-letter code. With 200 bookings, any search feels instant.

Think about: if the airline grows to 200K bookings, how many might the screen have to check to find yours? Does it matter where your booking sits in the list? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

As you read, look for:

1. Where a booking has to sit for a linear search to do the most work.
2. What happens to the worst-case checks when the list doubles from 4 bookings to 8.
3. Why a lookup like `bookings[3]` does about the same work for 4 bookings or 200K.

**[Start the reading: When the Crowd Grows →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/big-o-intuition/reading-1-whenthecrowdgrows/)** (about 23 minutes)

## Main takeaways

### Summary

* **Big-O is about growth, not seconds.** It answers one question: "As the input size grows, what happens to the amount of work?"
* **A linear search is O(n).** In the worst case, it checks all `n` items. So double the items means double the checks: 4 bookings take up to 4 checks, and 8 take up to 8. Using `in` on a list is a linear search too.
* **A lookup is O(1).** It jumps straight to the item. The work stays about the same as the data grows. A fast test on a few items can't show you which kind you have.

The picture below shows the worst-case steps as the bookings double. Watch the bars on the left grow, while the bars on the right stay at about 1 step.

![Two bar charts side by side with the same axes. The x-axis is the number of bookings: 25,000, 50,000, 100K, and 200K. The y-axis is worst-case steps, from 0 to 200K. Left, linear search, O(n): the bars rise to 25,000, 50,000, 100K, and 200K steps, doubling each time the bookings double. Right, lookup by code, O(1): every bar stays at about 1 step, too small to see.](images/m1a-growth-compare.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Big-O tells me how many seconds my code takes." | It tells you how the work *grows*. Double the bookings from 4 to 8, and the worst case grows from 4 checks to 8, on any computer. |
| "O(1) means it takes no time." | It means about the same work at any size: about 1 step for 4 bookings or 200K. That 1 step still takes a little time. |
| "O(n) means the code is slow." | A linear search over 5 items finishes almost at once. The work only becomes a problem when `n` is very large, like 200K. |
| "It was fast on 50 items, so it will be fast on 5M." | A small test doesn't show growth. An O(n) search on 5M items does up to 5M checks: 100K times as many as on 50. |
| "`in` is just one word, so it's one step." | On a list, `in` checks items one at a time from the start. `"ZZ1AA1" in bookings` checks all 4 bookings before it gives `False`. |

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
