## Module 1 Checkpoint

### 🎯 Ready for the Boss Battle (Project)?

No new reading here.

This is your **readiness gate**.

Your Inventory Tracker will require you to combine skills from across Module 1, so this Checkpoint tests whether you can retrieve those skills without being told exactly which lesson to use.

### Rules

**First attempt: no notes and no readings.**

For each challenge:

1. Answer from memory.
2. If you're wrong or stuck, open the Hint.
3. Try again.
4. Then open the Answer and explanation.

Anything you miss becomes a **Reload** before the Boss Battle.

---

# 🎮 Challenge 1 — Trace It

Don't run this code.

```python id="y9m5f4"
total = 0

for number in range(1, 4):
    if number > 1:
        total += number

print(total)
```

What prints?

Write the exact output.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Trace `number` through:

```text id="yr1wpe"
1
2
3
```

For each Iteration, evaluate:

```python id="b5s82j"
number > 1
```

Only update `total` when the condition is True.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The output is:

```text id="5mpt9w"
5
```

Trace:

```text id="4hvsfn"
number = 1 → condition False → total = 0
number = 2 → condition True  → total = 2
number = 3 → condition True  → total = 5
```

So:

**2 + 3 = 5**

</details>

---

# 🎮 Challenge 2 — Function + Scope

Consider:

```python id="0dhgva"
def calculate_total(price, quantity):
    total = price * quantity
    return total
```

The Function creates a Local Variable named:

```python id="9ujknr"
total
```

Does the Local Variable's **name** automatically become available everywhere else in the script after the Function runs?

Explain why or why not.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Separate these two ideas:

**Local Variable Name**

and

**Returned Value**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

`total` is a Local Variable created inside the Function's Local Scope.

The Function can return the **value** stored in `total`, but returning that value doesn't make the Local Variable name automatically available everywhere else.

For example:

```python id="62d97s"
result = calculate_total(5, 3)
```

stores the returned value in `result`.

</details>

---

# 🎮 Challenge 3 — Pick the Container

Your program needs to store inventory Items and frequently retrieve each Item using its unique Name.

Which is the stronger starting choice?

**A. List**

**B. Dictionary keyed by Item Name**

Don't answer with only the letter.

Explain why the structure matches the requirement.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

The requirement says:

> **Retrieve using a unique Name**

Which structure naturally supports:

**Key → Value**

relationships?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B. Dictionary keyed by Item Name**

A Dictionary naturally supports Key–Value relationships.

If Item Names are unique, each Name can serve as a Key associated with the corresponding Item.

This also prepares the program for Dictionary Lookup rather than requiring a one-by-one Linear Search through a List.

</details>

---

# 🎮 Challenge 4 — Make It Survive

Complete this conceptual pipeline:

```text id="9jv8fm"
Python Data
    ↓
?
    ↓
Stored Representation
    ↓
?
    ↓
Python Data
```

Name both missing processes.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

One process prepares data to be stored or transferred.

The other converts the stored representation back into usable data.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

```text id="rx3lvg"
Python Data
    ↓
Serialization
    ↓
Stored Representation
    ↓
Deserialization
    ↓
Python Data
```

**Serialization** creates a representation suitable for storage or transfer.

**Deserialization** converts that representation back into data the program can work with.

</details>

---

# 🎮 Challenge 5 — Validate the Transaction

Your transaction rules require:

```text id="cd50v2"
OPERATION,ITEM,QUANTITY
```

and Quantity must be non-negative.

Which transaction should be rejected?

```text id="6egqzt"
ADD,laptop,3
REMOVE,camera,-2
```

Explain the rule that determines your answer.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Check both:

**Structure**

and

**Quantity**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

This transaction should be rejected:

```text id="rzohbk"
REMOVE,camera,-2
```

Its Quantity is negative, so it fails the stated Validation rule.

The line having the expected number of fields does not automatically make the values valid.

</details>

---

# 🎮 Challenge 6 — Validation or Error Handling?

Match each situation.

### Situation A

Your program checks:

```python id="rvz8m7"
quantity >= 0
```

because negative Quantities violate your rules.

### Situation B

Your program attempts:

```python id="0r8ojp"
int(raw_quantity)
```

and handles the `ValueError` that occurs when `raw_quantity` is `"three"`.

Your choices:

**Validation**

**Error Handling**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Ask:

**Does this data meet my rules?**

versus:

**What should happen when this operation fails?**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**Situation A → Validation**

The program is checking the data against an explicit rule.

**Situation B → Error Handling**

The program is responding to an Exception raised during execution.

Validation and Error Handling can work together, but they have different responsibilities.

</details>

---

# 🎮 Challenge 7 — One Job at a Time

Your program needs to:

* Read transaction data.
* Validate transactions.
* Update inventory.
* Search inventory.
* Produce a summary.

A teammate proposes putting all five responsibilities into one giant Function.

What's the design concern?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think:

**Responsibilities → Testing → Debugging → Reuse**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

One Function would be responsible for several different jobs.

Separating major responsibilities into focused Functions can make each piece easier to understand, test, debug, and reuse.

The goal isn't to make every Function tiny.

The goal is to give Functions **clear responsibilities**.

</details>

---

# 🎮 Challenge 8 — Object Independence

Consider:

```python id="6i3jbf"
laptop = Item("Laptop", 4, "Electronics")
camera = Item("Camera", 9, "Electronics")

laptop.quantity = 2
```

Should `camera.quantity` automatically become `2`?

Explain why or why not.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Both Objects come from the same Class.

Are they the same **instance**?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

`laptop` and `camera` are independent Objects created from the same Class.

Changing an instance Attribute on `laptop` should not automatically change the corresponding Attribute on `camera`.

`camera.quantity` should remain:

```text id="6qgrfa"
9
```

</details>

---

# 🎮 Challenge 9 — When Does `__init__` Run?

A teammate says:

> **“`__init__` runs every time I use an Object.”**

Correct or incorrect?

Explain when `__init__` actually runs.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think about:

**Creating a new instance**

versus:

**Using an existing instance**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The statement is **incorrect**.

`__init__` runs as part of initializing a new instance when the Object is created.

It does not rerun every time you later access an Attribute or call another Method on that existing Object.

</details>

---

# 🎮 Challenge 10 — Complexity

Match each search strategy to its expected complexity.

### Linear Search by Item Name

### Dictionary Lookup by Key

Choices:

**O(n)**

**O(1) Average-Case**

Then explain both in plain language.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Which approach may need to inspect more Items as the inventory grows?

Which retrieves information using a Dictionary Key?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**Linear Search → O(n)**

The search may need to inspect more Items as the collection grows.

**Dictionary Lookup → O(1) Average-Case**

The average lookup work doesn't grow linearly with the number of Items in the same way.

Big-O describes how the amount of work **grows with Input Size**.

It does not describe which approach won one small timing experiment.

</details>

---

# 🐛 Challenge 11 — Attention to Detail

A Loop should process indexes:

```text id="fvsg0z"
0, 1, 2, 3, 4
```

but uses:

```python id="a2pnq8"
for index in range(4):
    process(index)
```

Name the bug precisely.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Write out the values produced by:

```python id="5u1hfd"
range(4)
```

Then compare them with the expected values.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

This is an **Off-by-One Error**.

`range(4)` produces:

```text id="frv8we"
0, 1, 2, 3
```

so index `4` is never processed.

The Loop runs successfully, but its behavior is incorrect.

</details>

---

# 🐛 Challenge 12 — Code Runs. Is It Correct?

An AI assistant generates code that:

* Runs without an Exception.
* Uses clear variable names.
* Includes comments.
* Produces output.

Is that enough evidence that the code is correct?

Explain what you should do next.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Retrieve your Module 0 rule:

**Confidence Is Not Evidence.**

Think:

**Expected Behavior → Actual Behavior**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

Successful execution and polished presentation do not prove that the program's logic is correct.

Define the Expected Behavior, test the code using known cases and important edge cases, and compare the Actual Behavior with the expected result.

If they differ, trace the code to locate where the behavior diverges.

</details>

---

# 🧠 Final Challenge — Design Before Code

Your Inventory Tracker needs to:

* Read transaction data.
* Validate transactions.
* Represent independent Items.
* Search inventory.
* Handle malformed input.
* Update inventory.
* Produce a summary.

Before writing the project, identify:

### One responsibility that belongs in a standalone Function

and:

### One responsibility that belongs on the `Item` Class

For each choice, explain:

> **Why does this responsibility belong there?**

There isn't one perfect architecture.

Your reasoning matters.

---

# 💼 Interview Arena

> **Walk me through how you would design a small Python program before you start coding it.**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Think:

**Requirements → Responsibilities → Data → Functions / Objects → Tests**

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

I start by identifying what the program needs to do and what data it needs to represent.

Then I separate the major responsibilities, decide which behaviors belong in standalone Functions and whether any data and behavior make sense as Objects.

I choose Data Structures based on the operations the program needs, define clear inputs and outputs for my Functions, and identify small test cases and edge cases before building everything together.

</details>

---

# 🏁 Readiness Check

You're ready for the Boss Battle when you can:

* Trace Control Flow without running the code.
* Explain Parameters, Return Values, and Local Scope.
* Choose a Data Structure based on a requirement.
* Explain Serialization and Deserialization.
* Validate input using explicit rules.
* Distinguish Validation from Error Handling.
* Design Functions with clear responsibilities.
* Create independent Objects.
* Explain when `__init__` runs.
* Compare O(n) Linear Search with O(1) Average-Case Dictionary Lookup.
* Identify an Off-by-One Error precisely.
* Verify code instead of assuming that running means correct.
* Decide what belongs in a Function versus a Class.

If you missed something, reload that specific concept before continuing.

---

# 🏆 Boss Battle (Project) Unlocked

You've practiced the pieces separately.

Now you'll combine them in one plain-Python program.

[**Start the Module 1 Boss Battle (Project) — Inventory Tracker →**](project.md)
