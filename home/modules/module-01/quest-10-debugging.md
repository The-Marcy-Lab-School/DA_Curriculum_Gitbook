# Quest 1.10 — Looks Right. Is It? Debugging (Days 18–19)

**Total time:** About 35 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · Load, save, and protect · **Check your work** ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* `range(3)` gives `0`, `1`, `2`: it starts at 0 and stops *before* 3, as you saw in [Trace the Path](quest-01-control-flow.md). This reading adds a start number: `range(2, 5)` gives `2`, `3`, `4`.
* A variable created inside a function exists only inside it, so using it outside raises a `NameError`. You saw this in [Build It Once, Use It Again](quest-02-functions-scope.md). In [Validate, Catch, Keep Going](quest-06-validation-errors.md), you learned that a bare `except:` catches every error, even real bugs.
* In Module 0's [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md), a chatbot said 64 bags, but the log added up to 46. An AI answer can sound sure and still be wrong. In this reading, an AI tool wrote the code, so you check it the same way.

## Introduction

A neat answer can still be wrong. For example, you buy 5 things at a store, and they cost $20 in all. But the receipt lists only 4 things and says $17. Nothing beeped. No error showed up. You only catch it because you know what you bought. In the picture below, look for the red item missing from the receipt on the left.

![Two receipts for the same 5 things: bread $3, milk $4, eggs $5, apples $6, and rice $2. Left, a receipt that skipped an item: bread is red and marked missing. Receipt total = $4 + $5 + $6 + $2 = $17, which is $3 short, and no error showed up. Right, a receipt with every item, all grey. Receipt total = $3 + $4 + $5 + $6 + $2 = $20, which matches the 5 things you bought.](images/receipt-missing-item.svg)

Code works the same way.

**Main takeaway:** Code can run with no error and still give a wrong answer. This is called a **logic error**. To catch it, first work out the **expected behavior**: the answer the code should give, found by hand. Then compare it with what the code prints.

**Why it matters at work:** Analysts check code before they trust its numbers, even code from a teammate or an AI (artificial intelligence) tool. For example, they check code to:

* make sure a monthly total adds up every row, not all but one
* review a teammate's function before its numbers go into a report
* find the bug in a function, a common interview task

If you skip the check, a wrong number goes into a report, and it looks just like a right one.

## Learning goals

After this reading, you should be able to say:

* I can work out the expected behavior of a small example by hand, then compare it with the actual behavior.
* I can name a bug precisely: an off-by-one error, a scope bug, an undefined attribute, or a bare `except:` that hides an error.
* I can confirm a fix or a refactor by running the same example again and comparing the output.

**Skills:** Attention to Detail

## Words to know

### What should the code do?: Expected and actual behavior

The examples use the receipt from the Introduction. Here are the 5 things you bought, in the order the cashier scanned them. In code, their prices are a list, in dollars:

`prices = [3, 4, 5, 6, 2]` (bread, milk, eggs, apples, rice)

Say the store's code adds up the receipt with a function, `receipt_total(prices)`. Its loop uses `range(1, len(prices))`. That skips bread, so the receipt says $17.

| Word | What it means | Example with the receipt |
| --- | --- | --- |
| **Bug** | Any gap between what code should do and what it actually does. Some bugs crash with an error. Others quietly print a wrong answer. | The code prints $17, but the right total is $20. |
| **Debugging** | Finding a bug, fixing it, and checking that the fix worked. | Find `range(1, len(prices))`, fix it, and rerun to get **$20**. |
| **Expected behavior** | What the code should do, worked out before you run it, often by hand on a small example. | $3 + $4 + $5 + $6 + $2 = **$20** |
| **Actual behavior** | What the code really does when it runs: the printed output, the returned value, or the error. | The code prints $20 − $3 = **$17**. |
| **Edge case** | An unusual input, like an empty list, a 0, or a missing value. Edge cases show bugs that normal inputs hide. | An item with no price, like eggs with a missing price tag |

Working out the expected behavior is the same habit as **predict** in [Trace the Path](quest-01-control-flow.md): say what the code will print before you run it, then compare.

### What went wrong?: Kinds of bugs

| Word | What it means | Example with the receipt |
| --- | --- | --- |
| **Logic error** | Code runs without crashing, but gives the wrong result. | It prints $17 instead of $20, with no error. |
| **Off-by-one error** | A loop or position that is one too many or one too few, so the code skips or repeats the first or last item. | `range(1, len(prices))` skips the first item, bread at **$3**. |
| **`range(start, stop)`** | Counts from `start` up to, but not including, `stop`. | With 5 items, `range(1, len(prices))` gives 1, 2, 3, 4, so it skips 0. |
| **Scope bug** | Using a variable where it doesn't exist, like outside the function that made it. Python raises a `NameError`. | `print(total)` outside `receipt_total`, the function that made `total` |
| **Undefined attribute** | Using an attribute that an object never got, often because of a typo in its name. Python raises an `AttributeError`. | In a `Receipt` class, `self.items_count`, when `__init__` set `item_count` |
| **Traceback** | The report Python prints when code crashes. Its last line names the error, so read it from the bottom up. | Last line: `NameError: name 'total' is not defined` |

### Can you tidy code without breaking it?: Refactoring

| Word | What it means | Example with the receipt |
| --- | --- | --- |
| **Refactor** | Changing how code is organized without changing what it does. The output must stay exactly the same. | After the fix, move a loop written twice into one function, `receipt_total`. Both versions print `Total: $20`. |

## Before you read

In the reading, you'll focus on a TV streaming app: an app for watching shows over the internet. It emails each viewer a monthly summary of minutes watched. An AI tool wrote the code. The code runs and prints neat numbers, but viewers send messages to say their numbers are wrong.

Think about: the code never crashed. How would you find out what's wrong? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. The expected total for the five viewing sessions (times a viewer watched something), and why the code prints a different number.
2. Which bugs crash with a traceback, and which ones quietly print a wrong answer.
3. How you confirm that a refactor didn't change what the code does.

**[Start the reading: Looks Right. Is It? →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/debugging/reading-1-looksrightisit/)** (about 24 minutes)

## Main takeaways

### Summary

* **Work out the expected answer first, then compare.** By hand, $3 + $4 + $5 + $6 + $2 = $20. The loop that used `range(1, len(prices))` printed $17, because it skipped the first item, bread: $20 − $3 = $17.
* **Some bugs are loud. Some are quiet.** A scope bug or an undefined attribute crashes, and the traceback names the line. An off-by-one error or a bare `except:` prints a believable wrong answer. Only your expected answer catches it.
* **Confirm every fix and every refactor.** Run the same example again and compare. Describe a bug precisely: "The line ___ does ___. It should ___."

The picture below shows these steps as a flow, using the receipt. Follow the path for a crash, then the path for a quiet wrong answer.

![A flow for finding a bug. Step 1: work out the expected behavior by hand: $3 + $4 + $5 + $6 + $2 = $20. Step 2: run the code. Then ask: did it crash? If yes, read the traceback from the last line up, because it names the line that failed, for example a NameError from a scope bug or an AttributeError from an undefined attribute. If no, compare the actual output with the expected one. The code printed $17, not $20, which is a logic error, so trace the loop. Examples: an off-by-one error from range(1, len(prices)), or a bare except that returns 0 and hides the problem. Both paths lead to step 3: fix one line, then rerun the same case. If it prints $20 now, the fix worked.](images/m1c-debug-flow.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "It ran with no error, so it's correct." | The receipt code ran with no error and printed $17. The right total is $20. Compare the output with your expected answer. |
| "A bare `except:` that returns 0 makes the code safer." | Say the eggs have no price. A bare `except:` that returns 0 counts them as $0. The receipt quietly says $15, not $20. Name the error you expect, like `except KeyError:`, and report it. |
| "`items_count` and `item_count` are close enough." | To Python, they're two different names. `self.items_count` raises an `AttributeError`, because `__init__` set `item_count`. |
| "I'll refactor the code, and that will fix the bug." | A refactor changes how code is organized, not what it does. Fix the $17 first. Then refactor, and check that it still prints $20. |
| "An AI tool wrote it, so it's already checked." | Check it the same way. Code from an AI tool can print $17 for the receipt when the expected answer is $20. |

### How this connects

* **Next:** In the Module 1 Checkpoint: Review and Practice, you'll answer short questions about every quest in this module. The ones you miss show you what to practice before the Boss Battle (Module Project).
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll test your own program on small examples where you already know the right answer. You'll fix anything that doesn't match before you call it done.

## Quick check

**1.** This loop should add up all 4 numbers in `prices`. The total comes out too small, with no error. Name the bug and fix it.

```python
total = 0
for i in range(len(prices) - 1):
    total += prices[i]
```

<details>
<summary>Answer</summary>

It's an off-by-one error. `range(len(prices) - 1)` gives `0`, `1`, `2`, so the last price is skipped. Loop over the items instead: `for price in prices:` then `total += price`. That leaves no position math to get wrong.

</details>

**2.** Does this code crash, or quietly print a wrong answer? What does Python say?

```python
class Item:
    def __init__(self, name):
        self.name = name

bread = Item("bread")
print(bread.nmae)
```

<details>
<summary>Answer</summary>

It crashes with `AttributeError: 'Item' object has no attribute 'nmae'`. It's an undefined attribute caused by a typo: `__init__` set `name`, not `nmae`. The last line of the traceback tells you this.

</details>

---

**Next:** [Module 1 Checkpoint: Review and Practice (Day 19)](checkpoint.md)
