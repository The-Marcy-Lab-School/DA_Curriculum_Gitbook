# Quest 1.1 — Trace the Path: Conditionals and Loops (Days 1–2)

**Total time:** about 60 minutes

**Building blocks:** **Decide and repeat** · Organize steps · Hold data · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Programs make choices, and they repeat work. For example, a teacher grades a stack of 30 tests. For each test, she asks one question: is the score 70 or higher? If yes, the test goes in the "pass" pile. If not, it goes in the "review" pile. She asks the same question 30 times, once per test.

A program does the same thing. Choosing a pile is a **conditional**. Doing it again for every test is a **loop**.

In this reading, you'll learn how to:

* make a program choose one path with `if`, `elif`, and `else`
* repeat steps with a `for` loop or a `while` loop
* put a loop inside a loop, or a choice inside a choice
* trace code by hand, so you can say what it prints before you run it

**Main takeaway:** Python runs the same steps in the same order every time. So if you trace code one step at a time, you can predict exactly what it will do.

**Why it matters at work:** Analysts go through rows of data and decide what to do with each one: keep it, fix it, or flag it (mark it so someone checks it). If a loop stops one row early, no error shows up. The numbers are just wrong.

## Learning goals

Check off each goal once you can do it.

- [ ] I can name the one branch of an `if`/`elif`/`else` chain that runs.
- [ ] I can count how many times a loop runs, and spot an off-by-one error.
- [ ] I can trace a nested loop or a nested conditional and predict every line it prints.

**Skills:** Control Flow & Loops

## Quick recall

You've already used the terminal and named data types. This reading puts both to work in Python.

* Recall that a **variable** is a named box that holds a value. `=` means "store," not "is equal to." You also sorted values into data types: text, whole numbers, decimals, and True/False. You did this in [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md). In this reading, comparisons like `runtime > 150` (is the movie longer than 150 minutes?) give back True or False.
* Recall that the terminal runs one typed command each time you press Enter, like `ls` or `cd`. You practiced this in [Meet Your Terminal](../module-00/quest-01-terminal.md). On your own laptop, you'll run a Python file the same way: `python3 theater_notes.py`.

## Words to know

This is your first Python reading. The [Module 1 Introduction](introduction.md#python-syntax-and-style) explains Python's rules for writing code, called its **syntax**. Indentation matters most on this page.

### How do you read Python code?: Basic syntax

| Word | What it means |
| --- | --- |
| **Script** | A small Python program saved in a file that ends in `.py`. |
| **Run a file** | Tell Python to do every line in the file, from top to bottom. |
| **Output** | What a program shows on the screen when it runs. |
| **`print()`** | A function that shows a value on the screen. A **function** is named code you run by writing its name and parentheses. |
| **String** | Text. It goes inside quotes. `98` is a number, but `"98"` is a string. |
| **List** | Several values kept in order, inside square brackets: `[98, 165, 122]`. |
| **Comparison** | A check that gives back True or False. `>` and `<` mean greater and less than. `>=` and `<=` add "or equal to." `==` asks "are these equal?" and `!=` asks "are these different?" |
| **Boolean** | A value that is either `True` or `False`. Every comparison gives back a Boolean. |
| **Comment** | A line that starts with `#`. It's a note for people. Python skips it. |
| **Block** | The lines under a line that ends with a colon (`:`). Each line in the block is pushed in by 4 spaces. That push is called **indentation**. It tells Python which lines belong together. |

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

**Code walkthrough:**

1. `temps = [68, 75, 81]` stores a list of three numbers in the variable `temps`.
2. `for temp in temps:` starts a loop. On each pass, `temp` holds the next number in the list.
3. `if temp > 80:` checks a comparison. It gives back True or False.
4. The two `print(...)` lines are each pushed in under their own branch. Only one of them runs on each pass.
5. The script prints `68 mild`, then `75 mild`, then `81 hot`.

### How does code choose?: Conditionals

A **condition** is a question with a True or False answer, like `temp > 80`.

| Word | What it means |
| --- | --- |
| **Conditional** | Code that checks a condition and picks which code runs next. |
| **Branch** | One possible path in a conditional: the block under an `if`, an `elif`, or an `else`. |
| **`if` / `elif` / `else`** | `if` checks the first condition. `elif` is short for "else if" and checks another condition. `else` runs only when every condition before it was False. |
| **Exactly one branch runs** | Python checks the chain from top to bottom. It runs the first branch whose condition is True, then skips the rest of the chain. |
| **Nested conditional** | An `if` written inside one branch of another `if`. Python checks the inner question only when it goes into the outer branch. |

### How does code repeat?: Loops

| Word | What it means |
| --- | --- |
| **Loop** | Code that repeats a block. |
| **`for` loop** | Repeats once for each item in a list, or for each number from `range()`. |
| **`while` loop** | Repeats as long as its condition stays True. Python checks the condition before every pass. |
| **Iteration** | One single pass through a loop. Four iterations means the loop body ran four times. |
| **Loop body** | The pushed-in code inside a loop. It runs once per iteration. |
| **Loop variable** | The name that holds the current item on each pass, like `temp` above. |
| **`range(n)`** | Makes the numbers to loop over. It starts at 0 and stops *before* `n`. So `range(3)` gives 0, 1, and 2: three numbers. |
| **Infinite loop** | A `while` loop whose condition never becomes False, so it never stops. The loop body must change something the condition checks. |
| **Nested loop** | A loop written inside another loop's body. The **outer loop** is on the outside. The **inner loop** sits in its body and runs all the way through on every outer pass. |

### How do you check your thinking?: Tracing

| Word | What it means |
| --- | --- |
| **Trace** | Follow the code by hand, one line and one pass at a time. Write down each variable's value as it changes. |
| **Predict** | Say what the code will print *before* you run it. Then run it and compare. |
| **Off-by-one error** | A loop that runs one time too many or one time too few. A start or stop number is one step off. Python shows no error. The result is just wrong by one. |
| **Edge case** | A value right at the edge of a rule. For example, a movie is exactly 150 minutes, and the rule says "over 150." Bugs (mistakes in code) often hide there. |

{% hint style="info" %}
**Count the first and last pass.** Off-by-one errors don't cause an error message. To catch them, trace the first pass and the last pass by hand, and count the lines that print.
{% endhint %}

## Before you read

In the first reading, you'll focus on a movie theater. A script gives a long time slot to any movie *over* 150 minutes. A **time slot** is a block of time on the theater's schedule for one movie. Every other movie gets a regular slot.

Think about: does a movie that is exactly 150 minutes get a long slot? Write down your first answer, then see if the reading agrees.

## Read

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
* **Count passes one at a time.** `range(n)` gives `n` numbers, from 0 up to `n - 1`. Check the first and last pass against what you meant, because that's where an off-by-one error shows up.
* **Read nested code from the outside in.** The inner loop finishes all its passes before the outer loop moves on. So the inner body runs (outer passes × inner passes) times. An inner `if` runs only when Python goes into the outer branch that holds it.

![On the left, the code runtimes.py: runtimes holds 98, 165, and 150, and a for loop with an if inside prints long slot for a runtime over 150 and regular slot otherwise. On the right, a trace with one row per pass. Pass 1: 98, False, prints 98 regular slot. Pass 2: 165, True, prints 165 long slot. Pass 3: 150, False, prints 150 regular slot. Pass 3 is the edge case, because 150 is not over 150.](images/m1a-trace-runtimes.svg)

![The order checkpoints.py prints its 12 lines. Outer pass 1, world Forest, runs inner checkpoints 1 to 4, printing lines 1 to 4. Then the outer loop moves on to Desert, lines 5 to 8, and then Ice, lines 9 to 12. 3 outer passes times 4 inner passes equals 12 lines printed.](images/m1a-nested-loop-order.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`range(6)` gives 1 through 6." | It gives 0 through 5. It starts at 0 and stops *before* 6. |
| "If two conditions are True, both branches run." | Only the first True branch runs. Python skips the rest of the chain. |
| "A `while` loop checks its condition once, at the start." | It checks before *every* pass. The loop body must change the value the condition uses. |
| "The outer and inner loops take turns, one pass each." | The inner loop runs all the way through on every outer pass. |
| "When the outer `if` is False, Python checks the inner `if` and finds it False too." | Python skips the inner `if`. It never checks it at all. |

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
