## Quest 1.7 — One Job at a Time (Days 11–12)

### 🎯 Your Mission

You've already built a Function that answers a focused question:

> **Is this transaction valid?**

Now the scaffolding starts to fade.

You'll design another Function that takes validated data and produces a useful summary.

The challenge isn't just getting the code to run.

It's deciding what the Function should be responsible for—and what it should **not** be responsible for.

**Target:** Use Loops and Conditional logic inside a single-purpose Function to summarize validated transaction data.

---

## 🔑 Vocabulary Mission

This time, most of the vocabulary is retrieval.

Be ready to use:

* **Function**
* **Parameter**
* **Return Value**
* **Accumulator**
* **Validation**
* **Single-Purpose Function**

Connect the ideas:

**Input → Function Responsibility → Processing → Return Value**

---

## 🎮 Warm-Up: What's the Job?

Imagine a Function named:

```python id="6g6m6x"
summarize_transactions(valid_transactions)
```

Its job is to count how many transactions are:

```text id="k0th8q"
ADD
REMOVE
SEARCH
```

Which responsibility probably **doesn't** belong inside this Function?

**A.** Loop through the validated transactions.

**B.** Count operation types.

**C.** Return a summary.

**D.** Rebuild the entire file-reading and Validation process from scratch.

Lock in your answer and explain why.

---

# 🎯 Main Mission — REQUIRED

## 🧩 One Job at a Time — Day 11

**Lecture Connection:** Summarizing Data With a Second Function

This reading deliberately gives you **less scaffolding** than your first Validation Function.

That's the point.

You're moving from:

**“Follow these steps.”**

toward:

**“Define the responsibility and design the steps.”**

[**Start Required Reading: One Job at a Time →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/summarizing-data-second-function/reading-1-onejobatatime/)

As you read, hunt for:

* How to define one clear Function responsibility.
* How a Loop can process a collection.
* How Conditionals can separate categories.
* How an Accumulator changes during Iteration.
* Why the Function should return a useful result.
* How this Function can consume data that another Function already validated.

When you return, be ready to answer:

> **What makes a Function single-purpose?**

---

# ⚡ Checkpoint 1: Define the Contract Before the Code

Imagine:

```python id="qaxfse"
summary = summarize_transactions(valid_transactions)
```

Before writing any Function body, define its contract.

### Input

What should go in?

### Job

What should the Function do?

### Output

What should come back?

### First Attempt

Write your contract without looking at a finished solution.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Don't start with Python syntax.

Complete these sentences:

> “This Function receives…”

> “Its one job is…”

> “It returns…”

</details>

### Second Attempt

Refine your contract.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

One reasonable contract is:

**Input:** A collection of already-validated transactions.

**Job:** Loop through the transactions and summarize their operation types.

**Output:** A summary that another part of the program can use.

The exact representation of the summary can vary.

The important design idea is that the Function has a **clear, limited responsibility**.

</details>

---

# 🔢 Checkpoint 2: Meet the Accumulator

Suppose you want to count `ADD` transactions.

You start with:

```python id="nnb2qn"
add_count = 0
```

Then, while looping through transactions, you increase `add_count` whenever you encounter an `ADD`.

What role is `add_count` playing?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Its value starts somewhere and changes as the Loop processes more data.

Retrieve today's vocabulary.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

`add_count` is acting as an **Accumulator**.

An Accumulator stores a running result as a Loop processes values.

For example:

```python id="5khbsn"
add_count = 0

for transaction in transactions:
    if transaction["operation"] == "ADD":
        add_count += 1
```

Each matching transaction updates the running count.

</details>

---

# 🎮 Build the Logic Before the Syntax

You receive these validated operation types:

```text id="64p8yg"
ADD
REMOVE
ADD
SEARCH
ADD
REMOVE
```

Without writing Python first, determine:

```text id="unmffg"
ADD    → ?
REMOVE → ?
SEARCH → ?
```

Then describe the algorithm in plain language.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Try:

1. Start each count at zero.
2. Inspect one transaction.
3. Identify its operation.
4. Update the matching count.
5. Repeat.
6. Return the summary.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The counts are:

```text id="h7z00b"
ADD    → 3
REMOVE → 2
SEARCH → 1
```

A plain-language algorithm could be:

1. Create a count for each operation type.
2. Loop through the validated transactions.
3. Check each transaction's operation.
4. Increase the matching count.
5. Return the completed summary.

Notice that you can reason about the algorithm **before** deciding on every line of Python syntax.

</details>

---

# 🧠 Single-Purpose Challenge

Consider this proposed Function:

```text id="tpxs9c"
summarize_transactions()
```

It:

* Opens the file.
* Reads every line.
* Converts quantities.
* Validates transactions.
* Handles malformed input.
* Counts operation types.
* Prints the final report.
* Saves another file.

What's the design concern?

### First Attempt

Don't just say:

> “It's too long.”

Explain the responsibility problem.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

How many different jobs is this one Function responsible for?

Could those jobs change independently?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The Function has **too many responsibilities**.

It's handling file input, conversion, Validation, Error Handling, Summarization, output, and storage.

Separating major responsibilities into focused Functions can make each piece easier to reason about, test, debug, and reuse.

The goal isn't:

> “Every Function must be tiny.”

The goal is:

> **Each Function should have a clear responsibility.**

</details>

---

# 🔗 Pipeline Challenge

You've now learned several pieces that can cooperate.

Put them into a reasonable order:

**Summarize**

**Deserialize / Read**

**Validate**

**Handle Expected Failures**

A simplified processing pipeline might look like:

```text id="x3nzt4"
Stored Data
    ↓
?
    ↓
?
    ↓
?
    ↓
Summary
```

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Ask:

1. How does data enter the program?
2. When should you determine whether it meets your rules?
3. When would Error Handling matter?
4. When should already-validated data be summarized?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

One reasonable conceptual pipeline is:

```text id="w2n67b"
Stored Data
    ↓
Read / Deserialize
    ↓
Validate
    ↓
Handle Expected Failures Where Needed
    ↓
Summarize Valid Data
```

Real programs may organize these responsibilities differently, and Error Handling can appear at multiple points.

The important idea is that the responsibilities **work together without becoming the same responsibility**.

</details>

---

# ⚔️ Recall & Practice — Day 12

**Lecture Connection:** Recall & Practice: Functions, Validation, `try` / `except`, Serialization

No new reading.

This is retrieval.

Try every round **without notes first**.

### Round 1 — Functions

Explain:

**Parameter → Function Body → Return Value**

### Round 2 — Scope

Why can't unrelated code automatically access every Local Variable created inside another Function?

### Round 3 — Serialization

What's the difference between Serialization and Deserialization?

### Round 4 — Validation

What question should a Validation Function answer?

### Round 5 — Error Handling

What's the purpose of `try` / `except`?

### Round 6 — Summarization

What's an Accumulator, and why might a summary Function need one?

### Round 7 — Put It Together

Explain one possible role for each:

**Serialization → Validation → Error Handling → Summary Function**

Anything you can't explain clearly becomes a **Reload**.

Review only that concept, close the material, and retrieve it again.

---

# 🐛 Debug the Candidate Answer

An interview candidate says:

> “A good Function should read the file, validate everything, handle every error, calculate the results, print them, and save them so all the code stays in one place.”

What's the weakness in that reasoning?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

“One place” can sound convenient.

But think about:

**Responsibilities → Testing → Debugging → Change**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

Keeping everything in one Function can mix many unrelated responsibilities.

That can make individual behaviors harder to test, debug, reuse, and change independently.

A stronger design usually separates major responsibilities into focused Functions with clear inputs and outputs.

</details>

---

# 💼 Interview Arena

> **What makes a Function single-purpose?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Ask yourself:

> **Can I describe this Function's responsibility in one clear sentence?**

Then connect that responsibility to its inputs and outputs.

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

A single-purpose Function has one clearly defined responsibility and inputs and outputs that support that job.

For example, a Validation Function can answer whether a transaction meets the program's rules, while a separate summary Function can take validated transactions and calculate a result.

Separating those responsibilities makes each Function easier to reason about and test.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Define a Function's **Input, Job, and Output** before coding.
* Explain what an **Accumulator** does.
* Use Loops and Conditionals inside a Function.
* Return a useful result instead of relying only on printing.
* Explain what makes a Function single-purpose.
* Explain why Validation and Summarization can be separate responsibilities.
* Connect Serialization, Validation, Error Handling, and Functions.
* Design a basic algorithm before translating it into Python syntax.
* Retrieve the Days 3–12 concepts without depending on the readings.

---

# 🔓 Next Unlock

So far, you've organized behavior into Functions and data into structures.

Next, you'll learn another way to organize a program:

> **What if related data and behavior belong together—and you need multiple independent versions of the same thing?**

[**Continue to Quest 1.8 — Meet the Objects (Days 13–15) →**](quest-08-oop.md)
