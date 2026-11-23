# Quest 1.10 — Looks Right. Is It? Debugging (Days 18–19)

**Total time:** about 35 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · Load, save, and protect · **Check your work** ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

A neat answer can still be wrong. For example, you buy 5 things at a store, but the receipt lists only 4. Nothing beeped. No error showed up. You only catch it because you know you bought 5.

Code works the same way. In this reading, you'll learn how to:

* work out the right answer by hand before you run the code
* find bugs (mistakes in code) that crash, or stop the program, by reading the error report from the bottom up
* find bugs that don't crash, but quietly print a wrong answer
* check a fix by running the same example again

**Main takeaway:** Code that runs is not always code that is correct. Decide what the answer should be first, then compare.

**Why it matters at work:** A wrong number in a report looks just like a right one. Analysts check code before they trust it, whether they wrote it, a teammate did, or an AI (artificial intelligence) tool did. "Find the bug in this function" is also a common interview task.

## Learning goals

After this reading, you should be able to say:

* I can work out the expected behavior of a small example by hand, then compare it with the actual behavior.
* I can name a bug precisely: an off-by-one error, a scope bug, an undefined attribute, or a bare `except:` that hides an error.
* I can confirm a fix or a refactor by running the same example again and comparing the output.

**Skills:** Attention to Detail

## Quick recall

* Recall that `range(3)` gives `0`, `1`, `2`: it starts at 0 and stops *before* 3, from [Trace the Path](quest-01-control-flow.md). This reading adds a start number: `range(2, 5)` gives `2`, `3`, `4`.
* Recall that a variable created inside a function exists only inside that function, from [Build It Once, Use It Again](quest-02-functions-scope.md). Using it outside raises a `NameError`. Recall too that a bare `except:` catches every error, even real bugs, from [Validate, Catch, Keep Going](quest-06-validation-errors.md).
* Recall that an AI answer can sound sure and still be wrong. In [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md), a chatbot said 64 bags, but the log added up to 46. In this reading, an AI tool wrote the code, so you check it the same way.

## Words to know

### What should the code do?: Expected and actual behavior

| Word | What it means |
| --- | --- |
| **Bug** | Any gap between what code should do and what it actually does. Some bugs crash with an error. Others quietly print a wrong answer. |
| **Debugging** | Finding a bug, fixing it, and checking that the fix worked. |
| **Expected behavior** | What the code should do, worked out before you run it, often by hand on a small example. |
| **Actual behavior** | What the code really does when it runs: the printed output, the returned value, or the error. |
| **Edge case** | An unusual input, like an empty list, a 0, or a missing value. Edge cases show bugs that normal inputs hide. |

Working out the expected behavior is the same habit as **predict** in [Trace the Path](quest-01-control-flow.md): say what the code will print before you run it, then compare.

### What went wrong?: Kinds of bugs

| Word | What it means |
| --- | --- |
| **Logic error** | Code runs without crashing, but gives the wrong result. |
| **Off-by-one error** | A loop or position that is one too many or one too few, so the code skips or repeats the first or last item. |
| **`range(start, stop)`** | Counts from `start` up to, but not including, `stop`. `range(1, 5)` gives 1, 2, 3, 4, so it skips 0. |
| **Scope bug** | Using a variable where it doesn't exist, like outside the function that made it. Python raises a `NameError`. |
| **Undefined attribute** | Using an attribute that an object never got, often because of a typo in its name. Python raises an `AttributeError`. |
| **Traceback** | The report Python prints when code crashes. Its last line names the error, so read it from the bottom up. |

### Can you tidy code without breaking it?: Refactoring

| Word | What it means |
| --- | --- |
| **Refactor** | Changing how code is organized without changing what it does, like moving a repeated loop into one function. The output must stay exactly the same. |

## Before you read

In the reading, you'll focus on a TV streaming app: an app for watching shows over the internet. It emails each viewer a monthly summary of minutes watched. An AI tool wrote the code. The code runs and prints neat numbers, but viewers send messages to say their numbers are wrong.

Think about: the code never crashed. How would you find out what's wrong? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. The expected total for the five viewing sessions (times a viewer watched something), and why the code prints a different number.
2. Which bugs crash with a traceback, and which ones quietly print a wrong answer.
3. How you confirm that a refactor didn't change what the code does.

**[Start the reading: Looks Right. Is It? →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/debugging/reading-1-looksrightisit/)** (about 24 minutes)

## Main takeaways

### Summary

* **Work out the expected answer first, then compare.** By hand, 50 + 42 + 95 + 38 + 61 = 286 minutes. The loop that used `range(1, len(sessions))` printed 236, because it skipped the first session.
* **Some bugs are loud. Some are quiet.** A scope bug or an undefined attribute crashes, and the traceback names the line. An off-by-one error or a bare `except:` prints a believable wrong answer. Only your expected answer catches it.
* **Confirm every fix and every refactor.** Run the same example again and compare. Describe a bug precisely: "The line ___ does ___. It should ___."

![A flow for finding a bug. Step 1: work out the expected behavior by hand: 50 + 42 + 95 + 38 + 61 = 286. Step 2: run the code. Then ask: did it crash? If yes, read the traceback from the last line up, because it names the line that failed, for example a NameError from a scope bug or an AttributeError from an undefined attribute. If no, compare the actual output with the expected one. The code printed 236, not 286, which is a logic error, so trace the loop. Examples: an off-by-one error from range(1, len(sessions)), or a bare except that returns 0 and hides the problem. Both paths lead to step 3: fix one line, then rerun the same case. If it prints 286 now, the fix worked.](images/m1c-debug-flow.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "It ran with no error, so it's correct." | A logic error runs fine and prints a wrong answer. Compare the output with your expected answer. |
| "A bare `except:` that returns 0 makes the code safer." | It hides the problem behind a 0 that looks real. Name the error you expect, like `except KeyError:`, and report it. |
| "`minutes_watch` and `minutes_watched` are close enough." | To Python, they're two different names. An object has only the attributes that were set on it. |
| "A refactor fixes a bug." | A refactor changes how code is organized, not what it does. Fix the bug first, then refactor, and check that the output stays the same. |
| "An AI tool wrote it, so it's already checked." | Check it the same way: expected answer first, then compare. |

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
class Viewer:
    def __init__(self, name):
        self.name = name

ana = Viewer("Ana")
print(ana.nmae)
```

<details>
<summary>Answer</summary>

It crashes with `AttributeError: 'Viewer' object has no attribute 'nmae'`. It's an undefined attribute caused by a typo: `__init__` set `name`, not `nmae`. The last line of the traceback tells you this.

</details>

---

**Next:** [Module 1 Checkpoint: Review and Practice (Day 19)](checkpoint.md)
