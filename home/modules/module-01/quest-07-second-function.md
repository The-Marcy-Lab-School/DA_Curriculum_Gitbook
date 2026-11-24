# Quest 1.7 — One Job at a Time: Writing a Second Function (Days 11–12)

**Total time:** About 35 minutes

**Building blocks:** Decide and repeat · **Organize steps** · Hold data · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* In [Build It Once, Use It Again](quest-02-functions-scope.md), you kept a running total with `total += loads`. `return` hands a value back to the caller, and a function with no `return` gives back `None`.
* **Unpacking** takes each tuple apart into separate variables, like `for code, time in finished:` in [Pick the Right Container](quest-04-data-structures.md). This reading loops over `(day, steps)` tuples the same way.
* Your validation function in [Validate, Catch, Keep Going](quest-06-validation-errors.md) checked each record (one entry, like one day's step count) against rules. This reading starts after that check is done.

## Introduction

Work goes better when each person has one clear job. For example, at a busy café, one worker takes orders, makes coffee, and cleans tables. Orders get mixed up, and it's hard to tell what went wrong. With one job each, everyone knows who to ask when something breaks.

Functions work the same way. A function with one job is easier to test, fix, and reuse. When someone asks for something new, you write a new function instead of making an old one longer.

**Main takeaway:** Give each function one job. A **single-purpose function** does one job that you can say in one sentence, like "summarize the week." Return its result, and write a new function for each new job.

**Why it matters at work:** Analysts split programs into small functions, so each part is easy to test and change. For example, they use one-job functions to:

* check a file in one function, and add up its numbers in another
* add a new report, like a weekly email, without changing code that already works
* test one step on a tiny example when a number looks wrong

If one function does every job, a change for one more report can break the parts that already worked.

## Learning goals

After this reading, you should be able to say:

* I can describe a function's contract (input, one job, output) before I write it.
* I can use an accumulator in a loop to build a total and a count.
* I can tell when a function is doing too many jobs, and move the extra job into its own function.

**Skills:** Functions & Modular Programming

## Words to know

### What counts as one job?: Single-purpose functions

The examples come from the reading's step tracker, with a goal of 8,000 steps a day.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Function** | A named, reusable block of code that runs when you call it. | `summarize_steps` |
| **Parameter** | A name in a function's `def` line that gets a value when the function is called. | `days` and `goal` in `def summarize_steps(days, goal):` |
| **Argument** | The value you pass in when you call the function. | In `summarize_steps(days, 8000)`, `8000` fills the parameter `goal`. |
| **Return value** | The value a function hands back to the code that called it, using `return`. | `{"total": 38070, "goal_days": 3}` |
| **Caller** | The line of code that calls a function and gets its return value. | `summary = summarize_steps(days, 8000)` |
| **Contract** | What a function takes in, its one job, and what it gives back. Decide it before you write any code. | In: good days and a goal. Job: summarize the week. Out: a summary dict. |
| **Single-purpose function** | A function that does one job, which you can describe in one sentence. That job can still give several related results, like a total and a count. | "`summarize_steps` sums up one week of steps." |
| **Summarizing** | Reporting useful facts, like a total, from data that was already checked. | Total for the week: **38,070 steps** |
| **Summary dict** | A dictionary that holds the results under names. | `{"total": 38070, "goal_days": 3}` |

The broader name for this idea is the **single-responsibility principle**: each piece of code should have one job.

You've used this idea before. In [Save the Story of Your Work](../module-00/quest-03-git.md), an atomic commit held one focused change. You could describe it in a short sentence. A single-purpose function is the same idea for code: one job, said in one sentence.

### Adding things up: Accumulators

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Accumulator** | A variable set before a loop and updated on every pass, like a running total. After the loop ends, it holds the answer. | `total` goes 0, then 6,200, then 15,320, and so on. |
| **Pass** | One time through the loop body. Another word for it is *iteration*. | 5 days means 5 passes. |
| **`+=`** | `total += steps` is short for `total = total + steps`. It takes the old total, adds `steps`, and stores the result back in `total`. | On Tuesday: 6,200 + 9,120 = **15,320 steps** |
| **Counter** | An accumulator that adds 1 each time something happens. | `goal_days += 1` on Tue, Wed, and Fri: **3 days** |
| **`continue`** | Skips the rest of the loop body for this pass and moves on to the next item. | In the teammate's version, it skips a day whose steps aren't a number. |

You've built a running total by hand. In the interactive reading for [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md), you added up the bags in the cleanup log: 9 + 12 + 7 + 10 + 8 = 46. An accumulator does the same adding, one pass at a time.

In the picture below, follow the reading's two accumulators, `total` and `goal_days`, through each pass. The goal is set to 8,000 steps.

![A worked example of summarize_steps with the goal set to 8,000 steps. Before the loop, total = 0 and goal_days = 0. Mon, 6,200 steps, misses the goal: total 6,200, goal_days 0. Tue, 9,120 steps, meets it: total 15,320, goal_days 1. Wed, 8,000 steps, meets it: total 23,320, goal_days 2. Thu, 4,300 steps, misses it: total 27,620, goal_days 2. Fri, 10,450 steps, meets it: total 38,070, goal_days 3. Days that met the goal are blue. After the loop, the function returns {"total": 38070, "goal_days": 3}.](images/m1b-accumulator-trace.svg)

The total is 6,200 + 9,120 + 8,000 + 4,300 + 10,450 = 38,070 steps. Wednesday counts as a goal day because the check is `steps >= goal`: 8,000 is *at least* 8,000. The total is in steps. `goal_days` is a count of days.

## Before you read

In the reading, you'll focus on a fitness tracker: an app that counts how many steps you walk each day. One function already checked a week of step counts and kept only the good days. Now you want a weekly summary: the total steps, and how many days met the step goal (the number of steps you aim for each day).

Think about: should the checking function also make the summary, or should the summary get its own function? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. The three things to decide before writing `summarize_steps`: what goes in, its one job, and what comes out.
2. What changes in the output when the goal changes, and what stays the same in the function.
3. Why the teammate's version, with `try` and `except` inside the summary, is a design problem even though it gives the right answer.

**[Start the reading: One Job at a Time →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/summarizing-data-second-function/reading-1-onejobatatime/)** (about 23 minutes)

Day 12 has no new reading. In class, you'll practice functions, validation, `try` and `except`, and saving data, without notes first.

## Main takeaways

### Summary

* **Decide the contract first.** Input: a list of good `(day, steps)` tuples and a goal. One job: summarize the week. Output: a summary dict.
* **An accumulator starts before the loop**, changes on every pass, and holds the answer after the loop. If you set it to 0 inside the loop, it starts over on every pass.
* **Return the result, and don't check twice.** Returning the dict lets another function print it, save it, or email it. `summarize_steps` trusts the days that `validate_days` already checked.

Here is the finished function from the reading:

```python
def summarize_steps(days, goal):
    total = 0
    goal_days = 0
    for day, steps in days:
        total += steps
        if steps >= goal:
            goal_days += 1
    return {"total": total, "goal_days": goal_days}

summary = summarize_steps(days, 8000)
```

<details>
<summary>Expand to walk through the code</summary>

1. The `def` line names two parameters: `days`, a list of good `(day, steps)` tuples, and `goal`, the daily step goal.
2. `total = 0` and `goal_days = 0` set up the two accumulators before the loop.
3. `for day, steps in days:` unpacks each tuple, so `day` gets a name like `"Mon"` and `steps` gets a number like `6200`.
4. `total += steps` adds this day's steps to the running total.
5. `if steps >= goal:` decides what to count. It isn't validation: the data was already checked.
6. `return` hands a summary dict back to the caller. It sits outside the loop, so it runs once, after every day.
7. In the call, `days` is the reading's list of five good days. The parameter `goal` is set to the argument `8000`. To use a different goal, change only the argument. The function stays the same.

</details>

The picture below shows where `summarize_steps` sits between two other functions. Look at the one job written under each function's name.

![Three functions in a chain. validate_days(), with the job "check records," passes good days, like [("Mon", 6200), ...], to summarize_steps(), with the job "summarize the week." summarize_steps() passes a summary, {"total": 38070, "goal_days": 3}, to print_week(), with the job "print the summary." Two dashed boxes branch from the summary: "New job: email the summary" and "New job: save it to a file," each a new function. Note: summarize_steps() returns its result, so new jobs never change it.](images/m1b-three-functions.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "One job means the function can give back only one result." | Count jobs, not results. The total (38,070 steps) and the goal days (3) describe the same week, so they're one job. |
| "Every function should check its data again, just to be safe." | Checking twice mixes two jobs. `validate_days` already kept only good days, so `summarize_steps` can trust them. |
| "`if steps >= goal` is validation." | It decides what to count. Thursday's 4,300 steps is good data. It just doesn't meet the goal. |
| "Printing the summary is the same as returning it." | Printing only shows it on the screen. Returning hands back `{"total": 38070, "goal_days": 3}`, so other code can save or email it. |
| "The app wants to email the summary, so I'll add that code to `summarize_steps`." | Emailing is a new job, so it gets its own function. That function takes the returned summary, and `summarize_steps` doesn't change. |

### How this connects

* **Next reading:** So far, you've kept data in containers and work in functions, separately. Next, you'll bundle related data and the functions that work on it into one unit. Then you'll make several separate copies of that unit, each with its own data.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll build your program from small functions. Each one will have a job you can say in one sentence, and each will pass its result to the next.

## Quick check

**1.** Using the reading's five days, what does `summarize_steps(days, 10000)` return?

<details>
<summary>Answer</summary>

`{"total": 38070, "goal_days": 1}`. The total doesn't depend on the goal. Only Friday (10,450 steps) reaches 10,000.

</details>

**2.** A teammate's `summarize_steps` ends with `print(summary)` and has no `return`. What does `result = summarize_steps(days, 8000)` store in `result`? Why is that a problem?

<details>
<summary>Answer</summary>

`None`, because a function with no `return` gives back `None`. The summary shows on the screen, but no other code can use it to save, compare, or email it.

</details>

---

**Next:** [Quest 1.8 — Meet the Objects: Classes and Objects (Days 13–15)](quest-08-oop.md)
