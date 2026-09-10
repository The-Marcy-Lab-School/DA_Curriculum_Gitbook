## Quest 1.6 — Validate, Catch, Keep Going (Days 9–10)

### 🎯 Your Mission

Real input isn't always clean.

A strong program doesn't blindly process every value and hope for the best.

First, it asks:

> **Does this input meet the rules my program expects?**

Then, when an operation can fail, it needs a deliberate way to respond.

**Target:** Validate incoming data and use Error Handling so expected failures can be handled without automatically crashing the entire program.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Validation**
* **Valid Input**
* **Invalid Input**
* **Malformed Input**
* **Exception**
* **Error Handling**
* `try`
* `except`

Keep these two jobs separate:

**Validation → Does the input meet our rules?**

**Error Handling → What should happen if an operation fails?**

---

## 🎮 Warm-Up: Would You Trust This?

Your program receives:

```text
ADD,laptop,3
REMOVE,charger,2
ADD,camera,-4
```

Suppose your program requires Quantity to be non-negative.

Should this line be processed normally?

```text
ADD,camera,-4
```

Choose:

**A.** Yes—the line has the right number of fields.

**B.** No—the program should check whether the values also satisfy its rules.

Explain your choice before starting the reading.

---

# 🎯 Main Mission — REQUIRED

Days 9–10 have **two required readings**.

These readings cover related but different responsibilities.

Complete both before moving to the Checkpoints.

---

## 🛡️ Part 1 — Trust, But Verify — Day 9

**Lecture Connection:** Writing Your First Validation Function, From Scratch

Today's first mission is about deciding whether incoming data satisfies your program's expectations.

[**Start Required Reading: Trust, But Verify →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/first-validation-function/reading-1-trustbutverify/)

As you read, hunt for:

* Why Validation belongs before blindly processing data.
* How a Validation Function can have one clear responsibility.
* How explicit rules make Validation testable.
* How a Boolean result can communicate whether data is valid.
* Why code that successfully receives input hasn't necessarily received **good** input.

When you return, be ready to answer:

> **What makes a Validation Function useful instead of just scattering checks throughout the program?**

---

## 🚨 Part 2 — Try It, Catch It, Keep Going — Day 10

**Lecture Connection:** Error Handling (`try` / `except`)

Validation can prevent some bad data from moving forward.

But operations can still fail.

Now focus on how Python lets your program respond to expected failures.

[**Start Required Reading: Try It, Catch It, Keep Going →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/error-handling/reading-1-tryitcatchitkeepgoing/)

As you read, hunt for:

* What an Exception represents.
* What belongs inside a `try` block.
* What an `except` block does.
* Why catching an error is different from pretending it never happened.
* Why useful Error Handling should be deliberate and specific.

When you return, be ready to answer:

> **What problem does `try` / `except` solve that Validation alone doesn't?**

---

# ⚡ Checkpoint 1: Valid or Invalid?

Your program expects transaction data with:

* The required fields.
* A recognized operation.
* A non-negative Quantity.

It receives:

```text
ADD,camera,-4
```

Should this transaction enter the collection of valid transactions?

### First Attempt

Apply the stated rules.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Don't stop after checking whether the line has the expected number of fields.

Check the **values** too.

Does `-4` satisfy the Quantity rule?

</details>

### Second Attempt

Try again before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

The Quantity is negative, so the transaction fails the stated Validation rule.

The line may look structurally similar to a valid transaction, but:

**Correct Shape ≠ Valid Data**

A Validation Function should apply the actual rules before the transaction is trusted.

</details>

---

# ⚡ Checkpoint 2: What Should the Function Return?

Suppose you write:

```python
def is_valid_transaction(transaction):
    # validation logic here
```

Which Return Value would make sense for a Function whose single responsibility is answering:

> **“Is this transaction valid?”**

**A.** A Boolean such as `True` or `False`.

**B.** Print `"I checked it!"` and return nothing.

### First Attempt

Choose one and explain why.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

What result would make it easy for another part of the program to write:

```python
if is_valid_transaction(transaction):
    # process it
```

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**A.**

A Boolean Return Value creates a clear Function contract:

```text
Input → Transaction
Job → Apply Validation Rules
Output → True or False
```

Then another part of the program can decide what to do with that result.

This reconnects to your Functions work from Days 3–5.

</details>

---

# 🐛 Failure Challenge

Imagine your program expects a Quantity it can convert to an integer.

It receives:

```text
ADD,camera,three
```

Then the program tries:

```python
quantity = int("three")
```

What happens?

More importantly:

**How should a program designed to process an entire batch respond to this expected kind of failure?**

### First Attempt

Choose the stronger behavior:

**A.** Let one malformed value terminate the entire batch automatically.

**B.** Handle the expected failure deliberately, report useful information, and continue when it is safe to do so.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Imagine this is transaction 4 out of 500.

Should one predictable malformed Quantity necessarily erase the opportunity to process the remaining valid transactions?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B.**

`int("three")` cannot perform the requested conversion and raises an Exception.

If this is an expected type of bad input, the program can handle that failure deliberately.

For example:

```python
try:
    quantity = int(raw_quantity)
except ValueError:
    print("Invalid quantity:", raw_quantity)
```

The goal is **not** to hide the problem.

The goal is to make the failure visible and respond appropriately rather than letting one expected malformed value automatically terminate the entire batch.

</details>

---

# 🧠 Validation or Error Handling?

For each situation, decide which idea is most directly involved.

### Situation 1

Your rules say Quantity cannot be negative.

You check whether:

```python
quantity >= 0
```

**Validation or Error Handling?**

### Situation 2

Python attempts:

```python
int(raw_quantity)
```

but `raw_quantity` contains `"three"`.

You respond to the resulting `ValueError`.

**Validation or Error Handling?**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

One asks:

**Does the data satisfy our rule?**

The other asks:

**What do we do when this operation raises an Exception?**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

### Situation 1 → Validation

You're checking the data against an explicit rule.

### Situation 2 → Error Handling

You're responding to an Exception raised while the program is executing an operation.

The ideas can work together, but they are not interchangeable.

</details>

---

# 🚫 Don't Catch Everything

Imagine this:

```python
try:
    process_transaction(transaction)
except:
    pass
```

The program now silently ignores anything that goes wrong.

Is that strong Error Handling?

Why or why not?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

If something fails:

* Will you know what failed?
* Will you know why?
* Could you accidentally hide a bug that wasn't caused by bad input?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

Silently catching every failure can hide useful information and make real bugs harder to detect.

Strong Error Handling should be deliberate about the failures it expects and should provide enough information to understand what happened.

Remember:

**Handle the Error ≠ Hide the Error**

</details>

---

# 🔁 Module 0 Callback: Confidence Is Not Evidence

Module 0 gave you a verification rule:

**Confidence Is Not Evidence.**

Apply that rule here.

An AI assistant gives you this Function:

```python
def is_valid_quantity(quantity):
    return quantity != 0
```

It says:

> “This correctly validates that quantities are non-negative.”

The code runs.

Should you trust the claim?

### First Attempt

Test the claim against the stated rule.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Try a value such as:

```text
-5
```

What does the Function return?

What **should** it return if negative Quantities are invalid?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

For `-5`:

```python
-5 != 0
```

is `True`.

So the Function would incorrectly accept a negative Quantity.

If the actual rule is **Quantity must be non-negative**, the implementation must be checked against that rule.

The fact that the code runs—and the fact that an AI assistant confidently explained it—doesn't prove that the logic is correct.

</details>

---

# 💼 Interview Arena

> **What's the difference between validating input and handling an Exception?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Use these two questions:

**Validation:** Does the data meet my program's rules?

**Error Handling:** What should my program do when an operation fails?

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

Validation checks whether input meets the rules my program expects before I trust or process it.

Exception handling gives my program a deliberate way to respond when an operation fails during execution.

They can work together. For example, I might validate that a Quantity is non-negative and also handle a `ValueError` if a Quantity can't be converted to an integer.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain **Validation**.
* Identify Invalid or Malformed Input using explicit rules.
* Explain why a Validation Function can return a Boolean.
* Explain what an **Exception** is.
* Explain the purpose of `try` and `except`.
* Distinguish Validation from Error Handling.
* Explain why handling an error doesn't mean hiding it.
* Explain why catching every possible error silently is risky.
* Test a Validation Function against edge cases instead of assuming it works.
* Apply **Confidence Is Not Evidence** to AI-generated code.

---

# 🔓 Next Unlock

You've built your first Validation Function and learned how to respond to expected failures.

Now the scaffolding starts to fade.

Your next job:

> **Design another Function with one clear responsibility.**

[**Continue to Quest 1.7 — One Job at a Time (Days 11–12) →**](quest-07-second-function.md)
