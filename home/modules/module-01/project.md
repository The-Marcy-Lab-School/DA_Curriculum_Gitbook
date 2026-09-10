## 🏆 Module 1 Boss Battle (Project) — Inventory Tracker

### Days 20–24

You've practiced the pieces.

Now you'll combine them into a working **plain-Python program**.

This Boss Battle is about more than making the program run.

You need to show that you can:

**Design → Build → Test → Debug → Explain**

---

# 🎯 Your Mission

Build a **command-line Inventory Tracker** for a small lending library or supply closet.

Your program will process a provided batch of inventory transactions, maintain a collection of Items, survive malformed input, and report the resulting inventory.

For this project:

**Use plain Python.**

**No pandas. No SQL.**

The goal is to demonstrate your Programming Fundamentals—not to solve the problem using tools you'll learn later.

---

# 📦 Required Evidence

Your finished project must demonstrate the following skills.

---

## 🏗️ 1. Build an `Item` Class

Define an `Item` Class that includes these Attributes:

```text id="njuhla"
name
quantity
category
```

Your Class must also include behavior that determines whether an Item is:

```text id="wspuhd"
low-stock
```

Create independent `Item` Objects from the Class.

Use the Class consistently.

Don't represent some inventory Items as `Item` Objects while other Items bypass the Class as unrelated loose data.

---

## 🧩 2. Separate Responsibilities With Functions

Use standalone Functions—not only Methods—to organize the major responsibilities in your program.

Your Functions should support responsibilities such as:

* Reading transaction data.
* Validating transactions.
* Updating inventory.
* Searching inventory.
* Producing summaries.

Avoid building one giant Function that controls the entire program.

Before writing a Function, be able to state:

**Input → Responsibility → Output**

---

## 🔁 3. Process Inventory Transactions

Your program must process operations such as:

```text id="hr6kq8"
ADD
REMOVE
SEARCH
```

Use **Loops** and **Conditionals** to determine what each transaction requires.

Your program should update or inspect the inventory based on the requested operation.

---

## 🛡️ 4. Validate Incoming Data

Don't automatically trust every transaction.

Apply explicit Validation rules before processing data.

Your program should identify malformed or invalid transaction lines rather than silently treating them as valid.

When something is invalid, your program should provide a **specific, useful message**.

Avoid messages like:

```text id="m7y4ba"
Something went wrong.
```

Prefer information that helps someone understand what failed.

---

## 🚨 5. Handle Expected Failures

One malformed line should not automatically destroy the entire batch when the failure can be handled safely.

Use appropriate Error Handling for operations that may raise expected Exceptions.

Remember:

**Handle the Error ≠ Hide the Error**

Your program should make failures visible while continuing when it is safe to do so.

---

# 🧪 Edge-Case Gauntlet

Don't test only the happy path.

Your program should be able to deal with cases such as:

### Malformed Line

A transaction doesn't follow the expected structure.

### Missing Information

A required field is missing.

### Empty File

There are no transactions to process.

### Missing Item

A `REMOVE` operation targets an Item that doesn't exist.

For each case, ask:

> **What should the program do?**

Then test whether it actually does that.

---

# 📊 Inventory Output

At the end of the program, print a formatted inventory summary.

Someone reading the output should be able to understand the resulting inventory state.

Your final output must also include a:

**Low-Stock Alert List**

Use the low-stock behavior from your `Item` Class rather than rebuilding unrelated low-stock logic throughout the program.

---

# 🧠 Complexity Reflection

Your project isn't complete when the program runs.

You also need to reason about one of its technical decisions.

Compare:

### Linear Search by Item Name

with:

### Dictionary-Keyed Lookup by Item Name

Your reflection must:

* Identify Linear Search as **O(n)**.
* Identify Dictionary Lookup as **O(1) Average-Case**.
* Explain the difference in plain language.
* State which approach your actual program uses.
* Explain why you chose it.

Don't submit only a generic definition such as:

> “O(n) is linear and O(1) is constant.”

Connect the explanation to **your Inventory Tracker**.

A stronger reflection answers:

> **As my inventory grows, what happens when my program searches for an Item by Name?**

---

# 🗺️ Sprint Map

Your Boss Battle runs across **Days 20–24**.

Each day has a different job.

---

## 🗓️ Day 20 — Sprint Day 1: Planning

Before building everything, design the program.

Decide:

**What belongs on the `Item` Object?**

**What belongs in standalone Functions?**

**What Data Structure will hold the inventory?**

**How will transactions move through the program?**

Trace the first few transaction lines **by hand** before writing the entire processing Loop.

Sketch a possible pipeline:

```text id="wm61wz"
Transaction Data
      ↓
Read
      ↓
Validate
      ↓
Process
      ↓
Update / Search Inventory
      ↓
Summary
```

Your exact architecture may differ.

The goal is to make deliberate decisions before coding.

---

## 🛠️ Day 21 — Sprint Day 2: Core Build

Build the central pieces.

Start small.

Test each major responsibility using examples where you already know the expected result.

Possible targets include:

* Creating `Item` Objects.
* Validating one transaction.
* Processing one operation.
* Updating one Item.
* Searching for one Item.

Don't wait until the entire program exists before testing anything.

**Build Small → Test → Continue**

Commit meaningful progress.

---

## 🔗 Day 22 — Sprint Day 3: Integration

Now connect the pieces.

Test how your:

**Functions + Objects + Control Flow + Data Structures**

behave together.

Run a small batch containing more than one type of operation.

Compare:

**Expected Inventory State**

with:

**Actual Inventory State**

When they differ, trace the program instead of guessing.

---

## ✨ Day 23 — Sprint Day 4: Polish

Stress-test the program.

Run your Edge-Case Gauntlet.

Then inspect the code itself.

Remove:

* Leftover debugging `print()` statements.
* Unused variables.
* Repeated logic that should be refactored.

Review your error messages.

Ask:

> **If this fails, will the message help someone understand what happened?**

Then review your names, Functions, and Object responsibilities.

Can another programmer follow the design?

---

## 🎤 Day 24 — Sprint Day 5: Review + Demo

Run the finished program.

Be ready to explain your work—not just show that it executes.

Prepare to discuss:

* How your program is organized.
* What responsibilities belong to standalone Functions.
* What responsibilities belong to the `Item` Class.
* Which Data Structure holds your inventory.
* One bug you found.
* How you located that bug.
* How you verified the fix.
* How your search approach behaves as the inventory grows.

The demo is part of the technical work.

---

# ⚠️ Boss Battle Traps

Before declaring victory, check for these common problems.

### 🪤 Trap 1 — The Mega-Function

One giant Function does everything.

**Counter:** Separate major responsibilities.

---

### 🪤 Trap 2 — One Bad Line Ends Everything

One expected malformed transaction crashes the entire batch.

**Counter:** Validate input and handle expected failures deliberately.

---

### 🪤 Trap 3 — Half OOP

Some Items use the `Item` Class while others bypass it.

**Counter:** Use your chosen representation consistently.

---

### 🪤 Trap 4 — Happy-Path Testing

You tested only perfect transactions.

**Counter:** Run the Edge-Case Gauntlet.

---

### 🪤 Trap 5 — It Runs, Ship It

The program executes, so you assume it's correct.

**Counter:** Compare Expected Behavior with Actual Behavior.

---

### 🪤 Trap 6 — Big-O From Memory

Your complexity reflection defines O(n) and O(1) but never discusses your actual program.

**Counter:** Tie the analysis to the search strategy your Inventory Tracker really uses.

---

### 🪤 Trap 7 — AI Said It's Fine

An AI assistant generates or reviews code and says it works.

**Counter:** Verify the claim yourself.

Remember:

**Confidence Is Not Evidence.**

---

# 🐛 Debugging Standard

When you find a bug, don't stop at:

> **“It didn't work.”**

Practice explaining:

### Expected

What should have happened?

### Actual

What happened instead?

### Location

Where did the behavior diverge?

### Cause

Why did it happen?

### Fix

What did you change?

### Verification

What evidence shows the fix worked?

This is stronger debugging—and stronger interview storytelling.

---

# 💼 Demo Arena

Be ready for this question:

> **Walk me through one technical decision you made in your Inventory Tracker and the evidence that supported it.**

Build your answer around:

**Problem → Decision → Evidence → Tradeoff**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Choose a real decision from your program.

For example:

* Data Structure choice.
* Function responsibility.
* Validation rule.
* Error Handling decision.
* Search strategy.
* Class design.

Explain the requirement first, then the decision you made because of it.

</details>

<details>
<summary>✅ Example Answer Structure — Open After You've Answered</summary>

**Problem:** Explain what your program needed to do.

**Decision:** Explain the technical choice you made.

**Evidence:** Describe the code, test, or behavior that supported the choice.

**Tradeoff:** Explain what you gained and what alternative you considered.

Use your **actual implementation** rather than memorizing a generic answer.

</details>

---

# 🤖 AI Use Check

If you use AI while building the project, you are still responsible for the code.

Before accepting AI-generated code:

1. Explain what the code is supposed to do.
2. Trace important logic.
3. Test a known case.
4. Test an edge case.
5. Inspect any unfamiliar syntax or method.
6. Compare the result with the project requirements.

You should be able to explain the final code without depending on the AI-generated explanation beside it.

---

# ✅ Boss Battle (Project) Checklist

Before submitting, verify that your project:

* [ ] Uses plain Python.
* [ ] Does not use pandas.
* [ ] Does not use SQL.
* [ ] Defines an `Item` Class.
* [ ] Includes `name`, `quantity`, and `category`.
* [ ] Includes low-stock behavior.
* [ ] Creates independent `Item` Objects.
* [ ] Uses the `Item` Class consistently.
* [ ] Uses standalone Functions.
* [ ] Gives major Functions clear responsibilities.
* [ ] Processes `ADD`, `REMOVE`, and `SEARCH`.
* [ ] Uses Loops and Conditionals.
* [ ] Validates transaction input.
* [ ] Reports malformed lines with specific, useful messages.
* [ ] Handles expected failures deliberately.
* [ ] Does not let one safely handleable malformed line crash the entire batch.
* [ ] Handles an empty file.
* [ ] Handles missing information.
* [ ] Handles a `REMOVE` operation for an Item that doesn't exist.
* [ ] Prints a formatted inventory summary.
* [ ] Prints a low-stock alert list.
* [ ] Tests edge cases—not only the happy path.
* [ ] Contains no leftover debugging prints.
* [ ] Contains no unused variables.
* [ ] Refactors unnecessary repeated logic.
* [ ] Identifies Linear Search as O(n).
* [ ] Identifies Dictionary Lookup as O(1) Average-Case.
* [ ] Connects the complexity reflection to the search approach actually used.
* [ ] Includes evidence that the final program was tested.

---

# 🔓 Portfolio Unlock

This project can give you evidence that you can:

* Write Control Flow.
* Design reusable Functions.
* Work with Python Data Structures.
* Validate input.
* Handle failures deliberately.
* Model data using Classes and Objects.
* Reason about Algorithmic Complexity.
* Debug systematically.
* Verify AI-generated code.
* Explain technical decisions.

Save the repository.

Keep your project explanation.

The code matters.

Your ability to explain **why you built it that way** matters too.

---

# 🎉 Module 1 Complete

You started this module tracing code by hand.

You finish it by designing, building, testing, debugging, and explaining a complete Python program.

Carry this workflow forward:

**Predict → Build → Test → Trace → Verify → Improve**
