# Quest 1.1 — Trace the Path: Conditionals and Loops (Days 1–2)

**Total time:** About 60 minutes

**Building blocks:** **Decide and repeat** · Organize steps · Hold data · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

You've already used the terminal and named data types. This reading puts both to work in Python.

* A **variable** is a named box that holds a value, and `=` means "store," not "is equal to." In Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), you also sorted values into types: text, whole numbers, decimals, and True/False. In this reading, comparisons like `runtime > 150` (is the movie longer than 150 minutes?) give back True or False.
* Each command you typed in Module 0's [Meet Your Terminal](../module-00/quest-01-terminal.md), like `ls` or `cd`, ran when you pressed Enter. On your own laptop, you'll run a Python file the same way: `python3 theater_notes.py`.

## Introduction

Programs make choices, and they repeat work. For example, a teacher grades a stack of 30 tests. For each test, she asks one question: is the score 70 or higher? If yes, the test goes in the "pass" pile. If not, it goes in the "review" pile. She asks the same question 30 times, once per test.

A program does the same thing. Choosing a pile is a **conditional**. Doing it again for every test is a **loop**.

**Main takeaway:** You can predict exactly what code will print by tracing it. To **trace** code means to follow it by hand, one line and one pass at a time. As you go, write down each value as it changes. This works because Python runs the same steps in the same order every time.

**Why it matters at work:** Analysts use loops and conditionals to go through rows of data and decide what to do with each row. For example, they use them to:

* keep only the rows they need, like the orders from this month
* **flag** a strange row, like a test score of 250 out of 100 (to flag means to mark it for someone to check)
* count rows, like how many movies run over 150 minutes

If a loop stops one row early, no error shows up. The count is just wrong by one.

## Learning goals

After this reading, you should be able to say:

* I can name the one branch of an `if`/`elif`/`else` chain that runs.
* I can count how many times a loop runs, and spot an off-by-one error.
* I can trace a nested loop or a nested conditional and predict every line it prints.

**Skills:** Control Flow & Loops

## Words to know

This is your first Python reading. The [Module 1 Introduction](introduction.md#python-syntax-and-style) explains Python's rules for writing code, called its **syntax**. Indentation matters most on this page.

### How do you read Python code?: Basic syntax

The examples come from the first reading's movie theater.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Script** | A small Python program saved in a file that ends in `.py`. | `theater_notes.py` |
| **Run a file** | Tell Python to do every line in the file, from top to bottom. | Type `python3 theater_notes.py` in the terminal. |
| **Output** | What a program shows on the screen when it runs. | `98 regular slot` |
| **`print()`** | A function that shows a value on the screen. A **function** is named code you run by writing its name and parentheses. | With `runtime = 98`, `print("Runtime:", runtime)` shows `Runtime: 98` |
| **String** | Text. It goes inside quotes. | `"Moonlight Run"`. `"98"` is a string, but `98` is a number. |
| **List** | Several values kept in order, inside square brackets. | `[98, 165, 122]` |
| **Comparison** | A check that gives back True or False. `>` and `<` mean greater and less than. `>=` and `<=` add "or equal to." `==` asks "are these equal?" and `!=` asks "are these different?" | `98 > 150` gives `False` |
| **Boolean** | A value that is either `True` or `False`. Every comparison gives back a Boolean. | `True` |
| **Comment** | A line that starts with `#`. It's a note for people. Python skips it. | `# Lines that start with # are notes for people.` |
| **Block** | The lines under a line that ends with a colon (`:`). Each line in the block is pushed in by 4 spaces. That push is called **indentation**. It tells Python which lines belong together. | The `print(...)` line pushed in under `for show in showtimes:` |

Two of these words are Python's names for data types you met in [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md):

* A **string** is Python's name for text. Quotes mark it, just like `"00417"`.
* A **Boolean** is Python's name for a true/false value.

For example, this short script uses most of these words:

```python
temps = [68, 75, 81]  # a list of numbers

for temp in temps:
    if temp > 80:
        print(temp, "hot")
    else:
        print(temp, "mild")
```

<details>
<summary>Expand to walk through the code</summary>

1. `temps = [68, 75, 81]` stores a list of three numbers in the variable `temps`.
2. `for temp in temps:` starts a loop. On each pass, `temp` holds the next number in the list.
3. `if temp > 80:` checks a comparison. It gives back True or False.
4. The two `print(...)` lines are each pushed in under their own branch. Only one of them runs on each pass.
5. The script prints `68 mild`, then `75 mild`, then `81 hot`.

</details>

### How does code choose?: Conditionals

A **condition** is a question with a True or False answer, like `temp > 80`.

The examples come from the first reading's lobby screen, which shows how soon a movie starts, and the second reading's game doors.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Conditional** | Code that checks a condition and picks which code runs next. | `if minutes_left >= 60:` |
| **Branch** | One possible path in a conditional: the block under an `if`, an `elif`, or an `else`. | `print("head over soon")`, under `elif minutes_left >= 15:` |
| **`if` / `elif` / `else`** | `if` checks the first condition. `elif` is short for "else if" and checks another condition. `else` runs only when every condition before it was False. | `if` 60 or more, `elif` 15 or more, `else` "starting now" |
| **Exactly one branch runs** | Python checks the chain from top to bottom. It runs the first branch whose condition is True, then skips the rest of the chain. | With `minutes_left = 25`, only `head over soon` prints. |
| **Nested conditional** | An `if` written inside one branch of another `if`. Python checks the inner question only when it goes into the outer branch. | `if key == "red":` inside `if key != "nothing":` |

### How does code repeat?: Loops

The examples come from the first reading's theater and the second reading's video game, which has 3 worlds with 4 checkpoints each.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Loop** | Code that repeats a block. | `for show in showtimes:` |
| **`for` loop** | Repeats once for each item in a list, or for each number from `range()`. | 3 showtimes, so the loop runs 3 times. |
| **`while` loop** | Repeats as long as its condition stays True. Python checks the condition before every pass. | `while minutes > 0:` prints 30, then 20, then 10. |
| **Iteration** | One single pass through a loop. | 3 showtimes means 3 iterations. |
| **Loop body** | The pushed-in code inside a loop. It runs once per iteration. | `print("Showing at", show)` |
| **Loop variable** | The name that holds the current item on each pass, like `temp` above. | `show` is `"4:15"`, then `"7:00"`, then `"9:45"`. |
| **`range(n)`** | Makes the numbers to loop over. It starts at 0 and stops *before* `n`. | `range(3)` gives 0, 1, and 2: three numbers. |
| **Infinite loop** | A `while` loop whose condition never becomes False, so it never stops. The loop body must change something the condition checks. | `while minutes > 0:` with no `minutes = minutes - 10` line |
| **Nested loop** | A loop written inside another loop's body. The **outer loop** is on the outside. The **inner loop** sits in its body and runs all the way through on every outer pass. | `for checkpoint in range(4):` inside `for world in worlds:` |

### How do you check your thinking?: Tracing

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Trace** | Follow the code by hand, one line and one pass at a time. Write down each variable's value as it changes. | Pass 1: `runtime` is 98. `98 > 150` is False, so it prints `98 regular slot`. |
| **Predict** | Say what the code will print *before* you run it. Then run it and compare. | "`showtimes.py` will print 3 lines." |
| **Off-by-one error** | A loop that runs one time too many or one time too few. A start or stop number is one step off. Python shows no error. The result is just wrong by one. | The theater has 7 screens. `range(6)` checks only 6 of them. |
| **Edge case** | A value right at the edge of a rule. Bugs (mistakes in code) often hide there. | A movie is exactly 150 minutes, and the rule says "over 150." |

{% hint style="info" %}
**Count the first and last pass.** Off-by-one errors don't cause an error message. To catch them, trace the first pass and the last pass by hand, and count the lines that print.
{% endhint %}

## Before you read

In the first reading, you'll focus on a movie theater. A script gives a long time slot to any movie *over* 150 minutes. A **time slot** is a block of time on the theater's schedule for one movie. Every other movie gets a regular slot.

Think about: does a movie that is exactly 150 minutes get a long slot? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

There are two readings. Do them in order.

### Reading 1 (Day 1)

As you read, look for:

1. Why only one branch of an `if`/`elif`/`else` chain runs, even when two conditions are True.
2. Why the theater's screen check prints six lines instead of seven, and how to fix it.
3. When a `while` loop checks its condition, and what in the loop body makes it stop.

**[Start the reading: Choose, Repeat, Trace →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/control-flow-conditionals/reading-1-chooserepeattrace/)** (about 23 minutes)

### Reading 2 (Day 2)

As you read, look for:

1. How many lines a loop inside a loop prints, and how you can count them without listing every one.
2. How indentation tells you which loop a `print()` line belongs to.
3. What Python does with an inner question when the answer to the outer question is no.

**[Start the reading: Inside the Inside →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/loops-conditionals/reading-1-insidetheinside/)** (about 22 minutes)

## Main takeaways

### Summary

* **Exactly one branch runs.** Python reads an `if`/`elif`/`else` chain from top to bottom. It runs the first branch whose condition is True and skips the rest.
* **Count passes one at a time.** `range(n)` gives `n` numbers, from 0 up to `n - 1`. For example, `range(7)` gives 0 to 6: 7 numbers. Check the first and last pass against what you meant, because that's where an off-by-one error shows up.
* **Read nested code from the outside in.** The inner loop finishes all its passes before the outer loop moves on. So the inner body runs (outer passes × inner passes) times. In `checkpoints.py`, that's 3 worlds × 4 checkpoints = 12 lines. An inner `if` runs only when Python goes into the outer branch that holds it.

The picture below traces the reading's `runtimes.py`, one pass per row. Look closely at pass 3, the edge case.

![On the left, the code runtimes.py: runtimes holds 98, 165, and 150, and a for loop with an if inside prints long slot for a runtime over 150 and regular slot otherwise. On the right, a trace with one row per pass. Pass 1: 98, False, prints 98 regular slot. Pass 2: 165, True, prints 165 long slot. Pass 3: 150, False, prints 150 regular slot. Pass 3 is the edge case, because 150 is not over 150.](images/m1a-trace-runtimes.svg)

The next picture shows the order `checkpoints.py` prints its lines. Follow the inner loop through each world before the outer loop moves on.

![The order checkpoints.py prints its 12 lines. Outer pass 1, world Forest, runs inner checkpoints 1 to 4, printing lines 1 to 4. Then the outer loop moves on to Desert, lines 5 to 8, and then Ice, lines 9 to 12. 3 outer passes times 4 inner passes equals 12 lines printed.](images/m1a-nested-loop-order.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`range(6)` counts 1, 2, 3, 4, 5, 6." | It gives 0, 1, 2, 3, 4, 5. It starts at 0 and stops *before* 6. That's why the theater's screen check printed 6 lines for 7 screens. |
| "Two of my conditions are True, so both of their lines print." | Only the first True branch runs. With `minutes_left = 90`, both `>= 60` and `>= 15` are True, but only `plenty of time` prints. |
| "A `while` loop checks its condition once, at the start, and then keeps going." | It checks before *every* pass. In `countdown.py`, `minutes` goes 30, 20, 10, then 0. `0 > 0` is False, so the loop stops after 3 lines. |
| "The loops take turns: Forest 1, Desert 1, Ice 1, then Forest 2." | The inner loop runs all the way through first: Forest 1, 2, 3, 4, then Desert 1. That makes 3 × 4 = 12 lines. |
| "The outer `if` is False, so Python checks the inner `if` and gets False too." | Python never checks the inner `if`. When `key` is `"nothing"`, it skips `key == "red"` and prints `no key`. |

### How this connects

* **Next reading:** You'll write a set of steps once, give it a name, and reuse it with different numbers. That way, you don't copy the same lines into many places.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll write code that goes through every record (one row of data) in a set of data. It will decide what to do with each one. Tracing it by hand is how you'll check it does what you meant.

## Quick check

**1.** What does this code print? Trace it before you open the answer.

```python
minutes_left = 60

if minutes_left >= 60:
    print("plenty of time")
elif minutes_left >= 15:
    print("head over soon")
else:
    print("starting now")
```

<details>
<summary>Answer</summary>

`plenty of time`. Both `60 >= 60` and `60 >= 15` are True. But Python runs only the first True branch, then skips the rest of the chain.

</details>

**2.** How many times does `print()` run here? What are the lines?

```python
for row in range(2):
    for column in range(2):
        print(row, column)
```

<details>
<summary>Answer</summary>

4 times: 2 outer passes × 2 inner passes. The inner loop finishes before the outer loop moves on. So the lines are `0 0`, `0 1`, `1 0`, `1 1`.

</details>

---

**Next:** [Quest 1.2 — Build It Once, Use It Again: Functions and Scope (Days 3–5)](quest-02-functions-scope.md)
