## Quest 1.2 — Build It Once, Use It Again (Days 3–5)

### 🎯 Your Mission

A program can work and still be difficult to understand, test, or reuse.

Functions help you divide a larger problem into smaller jobs with clear inputs and outputs.

Then **Scope** determines where the variables involved in those jobs can be used.

**Target:** Explain and use Functions, Parameters, Return Values, and Scope to organize reusable work.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Function**
* **Parameter**
* **Argument**
* **Return Value**
* **Local Variable**
* **Global Variable**
* **Scope**

Pay special attention to the relationships:

**Parameter ↔ Argument**

**Local Variable ↔ Scope**

**Function ↔ Return Value**

---

## 🎮 Warm-Up: One Giant Block?

Imagine a program that needs to:

**Read Data → Validate Data → Summarize Data → Print Results**

You could write all four jobs in one long block of code.

Or you could divide the work into smaller Functions.

Which approach would you rather debug?

Why?

Lock in your answer before the readings.

---

# 🎯 Main Mission — REQUIRED

Days 3–4 have **two required readings**.

Day 5 brings the ideas back together through retrieval and practice.

Complete both readings before moving to the Checkpoint.

## 🧩 Part 1 — Build It Once, Use It Again — Day 3

**Lecture Connection:** Functions, Parameters & Return Values

As you complete the reading, hunt for this workflow:

**Argument → Parameter → Function Body → Return Value**

Pay attention to:

* Why Functions are useful.
* How Parameters define expected inputs.
* How Arguments provide actual values.
* What `return` does.
* Why returning and printing are not the same thing.

[**Start Required Reading: Build It Once, Use It Again →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/functions-params/reading-1-builditonce/)

When you return, be ready to explain:

> **What information goes into a Function, and how can a result come back out?**

---

## 🔒 Part 2 — Who Can See This Variable? — Day 4

**Lecture Connection:** Local vs. Global Variables & Scope

Now focus on where variables exist.

Hunt for:

* Where a variable is created.
* Where that variable can be accessed.
* The difference between Local and Global Scope.
* Why a Local Variable doesn't automatically exist everywhere.

[**Start Required Reading: Who Can See This Variable? →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/local-global-vars/reading-1-whocanseethisvar/)

When you return, be ready to answer:

> **How can you determine whether a particular line of code can access a variable?**

---

# ⚡ Checkpoint 1: Parameter or Argument?

Consider:

```python
def greet(name):
    return f"Hello, {name}"

message = greet("Maya")
```

In this example:

**What is the Parameter?**

**What is the Argument?**

### First Attempt

Answer without reopening the reading.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Look in two places:

1. The Function **definition**.
2. The Function **call**.

</details>

### Second Attempt

Try again before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

`name` is the **Parameter**.

```python
def greet(name):
```

The Parameter is part of the Function definition.

`"Maya"` is the **Argument**.

```python
greet("Maya")
```

The Argument is the actual value supplied when the Function is called.

</details>

---

# ⚡ Checkpoint 2: Return or Print?

Which statement best describes `return`?

**A.** It only displays a value on the screen.

**B.** It sends a result back from a Function so other code can use it.

### First Attempt

Choose before opening the Hint.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Could another part of the program store and reuse the Function's result?

</details>

### Second Attempt

Choose again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B.**

A Return Value sends a result back to the code that called the Function.

For example:

```python
def double(number):
    return number * 2

result = double(4)
```

The returned value `8` can be stored in `result` and used elsewhere.

Printing and returning are different jobs.

</details>

---

# 🔒 Scope Check

Consider:

```python
def build_label(name):
    label = "Item: " + name
    return label
```

After the Function finishes, can unrelated code outside the Function automatically use the variable `label` by name?

### First Attempt

Explain why or why not.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Where was `label` created?

Think about **Local Scope**.

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

`label` is a **Local Variable** created inside `build_label()`.

The Function can return the **value** stored in `label`, but that doesn't make the Local Variable name `label` automatically available everywhere else.

This distinction matters:

**Returning a Value ≠ Making a Local Variable Global**

</details>

---

# 🐛 Bug Hunt: Wrong Scope

Consider:

```python
def calculate_total(price, quantity):
    total = price * quantity
    return total

calculate_total(5, 3)

print(total)
```

The programmer expects `15` to print.

What's the problem?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Where was `total` created?

Where is the programmer trying to access it?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

`total` is a Local Variable inside `calculate_total()`.

The Function returns its value, but the programmer doesn't store that returned value.

One correction is:

```python
result = calculate_total(5, 3)
print(result)
```

Now the returned value is stored in `result`, which can be used by the code outside the Function.

</details>

---

# ⚔️ Recall & Practice — Day 5

**Lecture Connection:** Recall & Practice: Loops, Conditionals, Functions

No new reading.

Retrieve what you've learned without reopening the previous pages.

### Round 1 — Control Flow

What determines whether an `if` branch executes?

### Round 2 — Loops

What changes from one Iteration to the next?

### Round 3 — Functions

Explain the difference between a Parameter and an Argument.

### Round 4 — Return Values

Why might another part of a program need a Function to `return` a value instead of only printing it?

### Round 5 — Scope

Why doesn't a Local Variable automatically become available outside its Function?

### Round 6 — Put It Together

Imagine a Function that loops through transaction quantities and returns the total.

Identify:

* The likely **Parameter**.
* The role of the **Loop**.
* A possible **Local Variable**.
* The **Return Value**.

Anything you can't explain clearly becomes a **Reload**.

Go back only to the concept you couldn't retrieve, then try again.

---

# 💼 Interview Arena

> **Why would you split a program into smaller Functions instead of writing one long script?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Think about:

**Responsibility → Testing → Debugging → Reuse**

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

I use smaller Functions to give different parts of the program clear responsibilities and defined inputs and outputs.

That makes individual pieces easier to understand, test, debug, and reuse than one long block of code.

It also helps me isolate a problem because I can test one Function instead of reasoning about the entire program at once.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain **Function**, **Parameter**, **Argument**, and **Return Value**.
* Distinguish a Parameter from an Argument in code.
* Distinguish `print()` from `return`.
* Explain Local and Global Scope.
* Explain why a Local Variable doesn't automatically leak outside a Function.
* Use a returned value outside the Function that produced it.
* Combine Functions with Loops and Conditionals.
* Explain why smaller, focused Functions can make code easier to test and debug.

If one of those still feels shaky, reload that concept before moving on.

---

# 🔓 Next Unlock

Your code works on a few values.

But what happens when the amount of data becomes much larger?

[**Continue to Quest 1.3 — When the Crowd Grows (Day 6) →**](quest-03-big-o-intuition.md)
