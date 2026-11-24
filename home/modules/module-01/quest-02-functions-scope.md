# Quest 1.2 — Build It Once, Use It Again: Functions and Scope (Days 3–5)

**Total time:** About 60 minutes

**Building blocks:** Decide and repeat · **Organize steps** · Hold data · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* In Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), `pet_of_the_week` held `"Biscuit"`, then `"Mango"`. A **variable** is a labeled box that keeps only its newest value. A function's inputs work the same way.
* You traced `minutes = minutes - 10` in the interactive reading for [Trace the Path](quest-01-control-flow.md). Python works out the right side first, then stores the result under the same name. Function bodies use the same kind of update.
* Indentation tells Python which lines belong to a block, as you saw in [Trace the Path](quest-01-control-flow.md). A function's steps are a block too, so where a line sits changes when it runs.

## Introduction

Some steps are worth writing down once. For example, a cook writes a pancake recipe on a card. Each time she cooks, she follows the same card. Only the number of people changes. If she improves the recipe, she fixes one card, not ten copies.

In code, that card is a **function**: a set of steps with a name that you can reuse.

**Main takeaway:** Write steps you repeat once, as a function, and call it each time you need them. A **function** is a named, reusable block of code. Values go in through its parameters, and one result comes back out with `return`.

**Why it matters at work:** Analysts use functions to run the same steps on many files or many rows. For example, they use them to:

* clean every file the same way, like removing blank rows
* work out a cost or a total the same way for every customer
* check each new file with the same rules

If the steps are copied instead, one missed copy can keep the old $3.50 price after it goes up to $4.00.

## Learning goals

After this reading, you should be able to say:

* I can write a function with parameters, call it with arguments, and use its return value.
* I can explain the difference between `print` and `return`.
* I can tell whether a variable is local or global, and say where it can be used.

**Skills:** Functions & Modular Programming

## Words to know

### What is a function?: Functions

**Modular** means built from small, separate pieces. **Modular programming** means splitting a program into small functions, each with one job. You can test and fix each piece on its own.

The examples come from the reading's laundromat, where one load of washing costs $3.50.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Function** | A named, reusable block of code. You define it once and call it as many times as you need. | `wash_cost`, which works out a bill |
| **Define** | Write the lines that create a function. Defining a function does *not* run it. | A file with only `def show_closing_notice():` and its body prints nothing. |
| **`def` line** | The first line of a function: `def`, the function's name, its inputs in parentheses, and a colon. | `def wash_cost(loads, price_per_load):` |
| **Function body** | The pushed-in lines under the `def` line. They are the function's steps. | `return loads * price_per_load` |
| **Call** | Run a function by writing its name and parentheses. Only a call runs the body. | `wash_cost(2, 3.5)` |
| **`return`** | Hands a value back to the line that called the function. It also ends the function right away. | `return loads * price_per_load` |
| **Return value** | The value a function hands back. The calling line can store it, add it to a total, or print it. | `wash_cost(2, 3.5)` gives back 2 × 3.5 = **7.0** dollars |
| **`None`** | Python's word for "no value." A function with no `return` line hands back `None`. | `show_cost(2, 3.5)` only prints, so it gives back `None`. |

Function names follow the same style as variable names: lowercase words joined by underscores, like `wash_cost`. This is called `snake_case`. The rule comes from PEP 8, Python's style guide. (PEP stands for "Python Enhancement Proposal.") See [the Module 1 Introduction](introduction.md#python-syntax-and-style).

### What goes in?: Parameters and arguments

You'll use these two words in every module after this one, so learn them exactly.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Parameter** | A name in the function's `def` line. It holds a spot for an input value. | `loads` in `def wash_cost(loads, price_per_load):` |
| **Argument** | The value passed in at a call. It fills the matching parameter. | `2` in `wash_cost(2, 3.5)` fills `loads`. |

So a parameter is a labeled box, like any variable. Each call puts a new argument inside it.

For example:

```python
def drink_cost(cups, price_per_cup):
    return cups * price_per_cup

total = drink_cost(3, 2.5)
print(total)  # 7.5
```

<details>
<summary>Expand to walk through the code</summary>

1. The `def` line defines a function named `drink_cost`. It has two parameters: `cups` and `price_per_cup`.
2. The body has one line. It multiplies the two parameters and returns the result.
3. `drink_cost(3, 2.5)` calls the function. This call sets the parameter `cups` to the argument `3`, and the parameter `price_per_cup` to the argument `2.5`.
4. The function returns `7.5`, and `total = ...` stores that return value in `total`.
5. `print(total)` shows `7.5` on the screen. The function itself printed nothing.

</details>

The picture below follows one call from the reading, `wash_cost(2, 3.5)`, through the same steps. Follow the arrows from the call into the function and back.

![On the left, the call saved = wash_cost(2, 3.5). An arrow goes into a function box labeled def wash_cost(loads, price_per_load). Step 1: each parameter gets its argument, so loads is 2 and price_per_load is 3.5. Step 2: the body runs, loads times price_per_load, 2 times 3.5 equals 7.0. Step 3: return hands back 7.0. An arrow goes back to the left, where saved now holds 7.0, the return value.](images/m1a-function-call.svg)

### New pieces of code in the readings

| Code | What it does |
| --- | --- |
| **`"WASHER " + "W-12"`** | `+` between two strings joins them: `"WASHER W-12"`. |
| **`str(7.0)`** | Turns a number into text: `"7.0"`. `+` can only join text to text. |
| **f-string** | Text with `f` before the opening quote. Python fills each `{name}` with that variable's value. `f"Cost: ${saved}"` becomes `Cost: $7.0`. |
| **`total += loads`** | A short way to write `total = total + loads`. |
| **`min(170, 150)`** | A function that gives back the smaller value: `150`. |

### Where can a name be used?: Scope

**Scope** is the part of a program where a name can be seen and used. Ask: "At this line, which names exist?"

The examples come from the second reading's parking tickets. A ticket costs a base amount plus $2 for each minute a car stays past its time.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Local variable** | A variable created inside a function, including its parameters. Only that function can see it. It stops existing when the function returns. | `ticket_cost`, created inside `ticket_price` |
| **Global variable** | A variable created outside every function. It exists for the whole program. Any function can read it. | `price_cap = 150`, at the top of the file |
| **`global`** | A word you can put in a function to change a global. The readings show it but suggest a parameter instead, because a parameter makes the call show everything the function needs. | `global tickets_issued` |

### What went wrong?: Error messages

You've read an error message before. In [Meet Your Terminal](../module-00/quest-01-terminal.md), `zsh: command not found: pdw` named the exact word the shell didn't know. Python's error messages work the same way: they name the problem.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Traceback** | What Python prints when it stops with an error. Read the last line first: it names the error. Then find the line number and the `^^^` marks under the part that failed. | Last line: `NameError: name 'ticket_cost' is not defined` |
| **`NameError`** | Code used a name that doesn't exist at that line. | `print(ticket_cost)` after `ticket_price` returned |
| **`UnboundLocalError`** | A function read a local variable before giving it a value. | `tickets_issued = tickets_issued + 1` inside a function |

## Before you read

In the first reading, you'll focus on a laundromat. A **laundromat** is a shop where people pay to use washing machines. One load of washing (one machine full of clothes) costs $3.50. The program works out each bill by copying the same math for every customer. Then the price goes up to $4.00.

Think about: what could go wrong when someone updates the price? How could you write the math so there's only one place to change? Write down your first answer, then see if the reading agrees.

## ⭐ Read

There are two readings, one on Day 3 and one on Day 4. Do them in order. Day 5 has no new reading. In class, you'll practice loops, conditionals, and functions together.

### Reading 1 (Day 3)

As you read, look for:

1. What happens when a file defines a function but never calls it.
2. In `machine_label("W-12")`, which part is the parameter and which is the argument.
3. Why `show_cost` hands back `None`, and why `total_loads` returns 12 instead of 36.

**[Start the reading: Build It Once, Use It Again →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/functions-params/reading-1-builditonce/)** (about 23 minutes)

### Reading 2 (Day 4)

As you read, look for:

1. Which names stop existing when `ticket_price` returns, and which value is kept.
2. Why a function that reads a global breaks when someone copies it into a new file.
3. Why `tickets_issued = tickets_issued + 1` inside a function causes an error.

**[Start the reading: Who Can See This Variable? →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/local-global-vars/reading-1-whocanseethisvar/)** (about 23 minutes)

## Optional reading (Side Quest)

Want to go further? This reading is optional. You don't need it for the checkpoint, but you can submit it for credit, the same way as a required reading.

**[Start the optional reading: Call Yourself Back: Recursion →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/recursion/reading-1-callyourselfback/)** (about 23 minutes)

## Main takeaways

### Summary

* **Define once, call many times.** Only a call runs a function's body. Each call can pass in different arguments without changing the function's code.
* **`return` hands a value back; `print` only shows it.** Store the return value to use it later. A `return` also ends the function, so check its indentation.
* **Local names live only during the call.** After a function returns, only its return value is kept. If a function needs a value, pass it in as a parameter instead of reading a global.

The picture below maps the names in the reading's `ticket_cap_global.py`. Look at which names sit inside the blue box, and which one makes it back out.

![A map of ticket_cap_global.py. A large grey box is the global scope: names created outside every function, which last the whole program. It holds price_cap = 150 and ticket_total = 150. Inside it, a blue box is the local scope of ticket_price, which exists only while the function runs. It holds the parameters base_cost = 90 and minutes_over = 40, and ticket_cost = 170, created in the body. An arrow shows the function can read price_cap. Another arrow shows return hands back 150 into ticket_total. An orange note says print(ticket_cost) outside the function gives a NameError, because the local name is gone after the return.](images/m1a-scope-map.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "My file has a `def` line, so the function ran." | The `def` line only defines it. `closing_notice.py` defines `show_closing_notice()` but never calls it, so it prints nothing. |
| "In `machine_label("W-12")`, `"W-12"` is the parameter." | `"W-12"` is the argument: the value you pass in. The parameter is `machine_id`, the name in the `def` line. |
| "`print` and `return` both give me the answer." | `print` only shows it. After `saved = show_cost(2, 3.5)`, the screen shows `This visit costs $7.0`, but `saved` holds `None`. |
| "After the function runs, I can still use `ticket_cost`." | It's gone after the return, so `print(ticket_cost)` gives a `NameError`. Use the stored return value, `ticket_total`. |
| "My function reads a global and it works, so it's fine." | It works only where that global exists. In a new file, `late_fee(3)` gives a `NameError`. `late_fee(3, 5)` passes the fee in and returns `15`. |

### How this connects

* **Next reading:** You'll look at how much work your code does as the data grows. For example, checking a list one item at a time takes longer as the list gets longer.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll split a program into small functions, each with clear inputs and a return value. Then you can test and fix each one on its own.

## Quick check

**1.** In this code, what is the parameter, and what is the argument?

```python
def greet(name):
    return f"Hello, {name}"

message = greet("Maya")
```

<details>
<summary>Answer</summary>

`name` is the parameter: it's the name in the `def` line. `"Maya"` is the argument: it's the value passed in at the call. This call sets the parameter `name` to the argument `"Maya"`.

</details>

**2.** The programmer expects this code to print `15`. What happens instead, and how would you fix it?

```python
def calculate_total(price, quantity):
    total = price * quantity
    return total

calculate_total(5, 3)
print(total)
```

<details>
<summary>Answer</summary>

It stops with a `NameError`. `total` is a local variable, so it stopped existing when the function returned. The return value was never stored. One fix:

```python
result = calculate_total(5, 3)
print(result)
```

</details>

---

**Next:** [Quest 1.3 — When the Crowd Grows: How Code Speed Scales (Day 6)](quest-03-big-o-intuition.md)
