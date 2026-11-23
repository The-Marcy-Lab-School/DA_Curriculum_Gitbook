# Quest 1.2 — Build It Once, Use It Again: Functions and Scope (Days 3–5)

**Total time:** about 60 minutes

**Building blocks:** Decide and repeat · **Organize steps** · Hold data · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Some steps are worth writing down once. For example, a cook writes a pancake recipe on a card. Each time she cooks, she follows the same card. Only the number of people changes. If she improves the recipe, she fixes one card, not ten copies.

In code, that card is a **function**: a set of steps with a name that you can reuse.

In this reading, you'll learn how to:

* write a function once and use it many times
* pass values into a function, and get one result back out
* tell a function's own variables apart from the ones the whole program can use

**Main takeaway:** A function keeps one job in one place. Values go in through its inputs, and one result comes back out with `return`.

**Why it matters at work:** Analysts run the same steps on many files: clean, check, and sum. If those steps are copied into many places, one missed copy gives a wrong number. A function puts the fix in one place.

## Learning goals

Check off each goal once you can do it.

- [ ] I can write a function with parameters, call it with arguments, and use its return value.
- [ ] I can explain the difference between `print` and `return`.
- [ ] I can tell whether a variable is local or global, and say where it can be used.

**Skills:** Functions & Modular Programming

## Quick recall

* Recall that `minutes = minutes - 10` works out the right side first. Then it stores the result back under the same name. You traced it in [Trace the Path](quest-01-control-flow.md). Function bodies use the same kind of update.
* Recall that indentation tells Python which lines belong to a block, from [Trace the Path](quest-01-control-flow.md). A function's steps are a block too. Where a line sits changes when it runs.

## Words to know

### What is a function?: Functions

**Modular** means built from small, separate pieces. **Modular programming** means splitting a program into small functions, each with one job. You can test and fix each piece on its own.

| Word | What it means |
| --- | --- |
| **Function** | A named, reusable block of code. You define it once and call it as many times as you need. |
| **Define** | Write the lines that create a function. Defining a function does *not* run it. |
| **`def` line** | The first line of a function: `def`, the function's name, its inputs in parentheses, and a colon. |
| **Function body** | The pushed-in lines under the `def` line. They are the function's steps. |
| **Call** | Run a function by writing its name and parentheses, like `wash_cost(2, 3.5)`. Only a call runs the body. |
| **`return`** | Hands a value back to the line that called the function. It also ends the function right away. |
| **Return value** | The value a function hands back. The calling line can store it, add it to a total, or print it. |
| **`None`** | Python's word for "no value." A function with no `return` line hands back `None`. |

Function names follow the same style as variable names: lowercase words joined by underscores, like `wash_cost`. This is called `snake_case`. The rule comes from PEP 8, Python's style guide. See [the Module 1 Introduction](introduction.md#python-syntax-and-style).

### What goes in?: Parameters and arguments

You'll use these two words in every module after this one, so learn them exactly.

| Word | What it means |
| --- | --- |
| **Parameter** | A name in the function's `def` line. It holds a spot for an input value. |
| **Argument** | The value passed in at a call. It fills the matching parameter. |

For example:

```python
def drink_cost(cups, price_per_cup):
    return cups * price_per_cup

total = drink_cost(3, 2.5)
print(total)  # 7.5
```

**Code walkthrough:**

1. The `def` line defines a function named `drink_cost`. It has two parameters: `cups` and `price_per_cup`.
2. The body has one line. It multiplies the two parameters and returns the result.
3. `drink_cost(3, 2.5)` calls the function. This call sets the parameter `cups` to the argument `3`, and the parameter `price_per_cup` to the argument `2.5`.
4. The function returns `7.5`, and `total = ...` stores that return value in `total`.
5. `print(total)` shows `7.5` on the screen. The function itself printed nothing.

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

| Word | What it means |
| --- | --- |
| **Local variable** | A variable created inside a function, including its parameters. Only that function can see it. It stops existing when the function returns. |
| **Global variable** | A variable created outside every function. It exists for the whole program. Any function can read it. |
| **`global`** | A word you can put in a function to change a global. The readings show it but suggest a parameter instead, because a parameter makes the call show everything the function needs. |

### What went wrong?: Error messages

| Word | What it means |
| --- | --- |
| **Traceback** | What Python prints when it stops with an error. Read the last line first: it names the error. Then find the line number and the `^^^` marks under the part that failed. |
| **`NameError`** | Code used a name that doesn't exist at that line. For example, it used a local variable after its function returned. |
| **`UnboundLocalError`** | A function read a local variable before giving it a value. |

## Before you read

In the first reading, you'll focus on a laundromat. One load of washing costs $3.50. The program works out each bill by copying the same math for every customer. Then the price goes up to $4.00.

Think about: what could go wrong when someone updates the price? How could you write the math so there's only one place to change? Write down your first answer, then see if the reading agrees.

## Read

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

## Main takeaways

### Summary

* **Define once, call many times.** Only a call runs a function's body. Each call can pass in different arguments without changing the function's code.
* **`return` hands a value back; `print` only shows it.** Store the return value to use it later. A `return` also ends the function, so check its indentation.
* **Local names live only during the call.** After a function returns, only its return value is kept. If a function needs a value, pass it in as a parameter instead of reading a global.

![A map of ticket_cap_global.py. A large grey box is the global scope: names created outside every function, which last the whole program. It holds price_cap = 150 and ticket_total = 150. Inside it, a blue box is the local scope of ticket_price, which exists only while the function runs. It holds the parameters base_cost = 90 and minutes_over = 40, and ticket_cost = 170, created in the body. An arrow shows the function can read price_cap. Another arrow shows return hands back 150 into ticket_total. An orange note says print(ticket_cost) outside the function gives a NameError, because the local name is gone after the return.](images/m1a-scope-map.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Python runs a function when it reaches the `def` line." | The `def` line only defines it. Only a call runs the body. |
| "The parameter is the value I pass in." | The parameter is the name in the `def` line. The value you pass in is the argument. |
| "`print` and `return` do the same job." | `print` shows a value to a person. `return` hands it back to the code. A function with no `return` gives back `None`. |
| "After a function runs, I can use its local variables." | They're gone. Store the return value in a variable instead. |
| "Reading a global inside a function is always fine." | It works only where that global exists. A parameter makes the call show everything the function needs. |

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
