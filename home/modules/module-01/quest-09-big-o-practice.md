## Quest 1.9 — Lookups Matter (Days 16–17)

### 🎯 Your Mission

Back on Day 6, you built your first Big-O intuition:

> **What happens to the amount of work as the input grows?**

Now you'll connect that question to real Python code.

You'll compare two ways to find an Item:

**Linear Search → Check Items one by one**

**Dictionary Lookup → Retrieve an Item using its Key**

Both can work.

But they don't scale the same way.

**Target:** Compare Linear Search with Dictionary Lookup and explain why their growth behavior differs as inventory size increases.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Linear Search**
* **Dictionary Lookup**
* **Input Size**
* **O(n)**
* **O(1) Average-Case**
* **Scale**
* **Complexity**

Don't stop at the notation.

You should be able to translate:

**O(n)**

and

**O(1) Average-Case**

into plain language.

---

## 🎮 Warm-Up: The Inventory Grows

Imagine your inventory contains **10 Items**.

Then it grows to **10,000 Items**.

You need to find `"camera"`.

### Approach A — Linear Search

Check each Item one by one until the Name matches.

### Approach B — Dictionary Lookup

Use `"camera"` as a Dictionary Key.

Which approach do you predict will be more affected as the inventory grows?

Explain **why** before starting the reading.

---

# 🎯 Main Mission — REQUIRED

## 🔎 Lookups Matter — Day 16

**Lecture Connection:** Big-O in Practice: Linear Scan vs. Dict Lookup, With a Partner

This is where your Day 6 Big-O intuition meets your Day 7 Data Structures work.

[**Start Required Reading: Lookups Matter →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/python-data-structures/reading-2-lookupsmatter/)

As you read, hunt for:

**Linear Search → O(n)**

versus:

**Dictionary Lookup → O(1) Average-Case**

Pay attention to:

* What happens during a Linear Search.
* Why the amount of Linear Search work can grow with the collection.
* How Dictionary Keys support lookup.
* Why Dictionary Lookup is described as O(1) Average-Case.
* Why tiny examples can hide meaningful differences.
* Why the Data Structure you choose affects the operations available to your program.

When you return, be ready to answer:

> **Why can Dictionary Lookup scale differently from Linear Search?**

---

# ⚡ Checkpoint 1: Name the Complexity

Match each approach with its expected complexity.

### Linear Search by Item Name

**A. O(n)**

**B. O(1) Average-Case**

### Dictionary Lookup by Key

**A. O(n)**

**B. O(1) Average-Case**

### First Attempt

Choose both before opening the Hint.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Which approach may need to inspect more Items as the collection grows?

Which approach uses a Key to access the desired entry?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**Linear Search → O(n)**

A Linear Search may need to inspect Items one by one. As the number of Items grows, the amount of work can grow with it.

**Dictionary Lookup → O(1) Average-Case**

A Dictionary can retrieve a Value using its Key without performing the same one-by-one scan through every entry.

That's why its lookup is described as **O(1) Average-Case**.

</details>

---

# 🔎 Trace the Linear Search

Consider:

```python id="5xv9y8"
items = ["laptop", "charger", "camera", "tablet"]

target = "tablet"

for item in items:
    if item == target:
        print("Found")
        break
```

If `"tablet"` is last, how many Item Names are checked?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Trace the Loop:

```text id="wcn9fy"
laptop
charger
camera
tablet
```

When does the condition become True?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

All **4 Item Names** are checked before `"tablet"` is found.

If the target remains near the end while the collection grows, the search may need to perform more checks.

That's the connection to **O(n)**.

</details>

---

# 🗝️ Compare the Dictionary

Now consider:

```python id="4mmkyp"
inventory = {
    "laptop": 4,
    "charger": 12,
    "camera": 7,
    "tablet": 2
}

quantity = inventory["tablet"]
```

Does this code explicitly Loop through each Dictionary entry until it reaches `"tablet"`?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Look at the operation:

```python id="jy4w68"
inventory["tablet"]
```

Is the code performing the same one-by-one scan you saw in the Linear Search?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

The code uses `"tablet"` as a Dictionary Key to retrieve its associated Value.

This lookup is **O(1) Average-Case**.

The important comparison is:

**Linear Search → Work can grow with n**

**Dictionary Lookup → Average lookup work does not grow linearly with n**

</details>

---

# 🐛 Misconception Check: Tiny Isn't the Point

A teammate tests both approaches on **three Items**.

The Linear Search happens to finish first.

They conclude:

> **“Linear Search has better Big-O.”**

What's wrong with that conclusion?

### First Attempt

Use what you learned on Day 6.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Does Big-O describe which approach won **one timing test**?

Or does it describe how the amount of work grows as Input Size grows?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A single timing result on a tiny collection does **not** determine Big-O.

Linear Search is **O(n)** because the amount of searching can grow with the number of Items.

Dictionary Lookup by Key is **O(1) Average-Case** because its average lookup work doesn't grow in the same linear way with the number of stored Items.

Remember:

**Big-O describes growth—not the winner of one stopwatch test.**

</details>

---

# ⏱️ Stress-Test Your Code — Day 17

**Lab Connection:** Stress-Test Your Code: Timing & Efficiency

Now take the comparison beyond a tiny example.

Use increasingly larger collections and compare the two lookup approaches.

For example, you might test with:

```text id="w2x5mx"
10 Items
100 Items
1,000 Items
10,000 Items
```

Your goal is **not** to prove Big-O using one timing result.

Instead, use measurements as evidence while asking:

* What happens as Input Size grows?
* Does the observed pattern match my complexity prediction?
* Am I comparing equivalent work?
* Could other factors affect an individual timing measurement?

Keep the distinction clear:

**Timing Experiment → Observed Evidence**

**Big-O → Growth Model**

---

# 🧠 Decision Challenge

Your Inventory Tracker needs to search for Items by unique Name frequently.

You have two possible designs.

### Design A

Store Items in a List and perform a Linear Search by Name.

### Design B

Store Items in a Dictionary keyed by Item Name.

Which would you choose?

Don't answer only:

> **“Dictionary because it's faster.”**

Defend the choice using:

**Requirement → Data Structure → Lookup Strategy → Complexity**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

The requirement is frequent retrieval by a unique Item Name.

Which structure naturally provides a Key for that operation?

Then connect the operation to its expected complexity.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A Dictionary is a strong choice if the program frequently retrieves Items using their unique Names.

The Item Name can serve as the Dictionary Key, supporting **O(1) Average-Case** lookup.

With a List, searching by Name generally requires a **Linear Search**, which is **O(n)**.

The important reasoning chain is:

**Frequent Lookup by Unique Name → Dictionary Key → Dictionary Lookup → O(1) Average-Case**

</details>

---

# ⚖️ Don't Turn Big-O Into a Rulebook

Does this mean:

> **“Never use Linear Search.”**

No.

A simple List and Linear Search may be perfectly reasonable for a small program or a situation where lookup performance isn't important.

Complexity is one factor in a technical decision.

Your job is to understand the tradeoff and connect your choice to the actual requirements.

---

# 💼 Interview Arena

> **Why can Dictionary Lookup scale better than Linear Search?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Use both technical terms:

**O(n)**

**O(1) Average-Case**

Then translate them into plain language.

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

With Linear Search, I may need to inspect more Items as the collection grows, so searching is O(n).

A Dictionary Lookup by Key is O(1) Average-Case, so its average lookup work doesn't grow linearly with the number of stored Items.

That difference becomes more important as the collection gets larger, especially when the program performs frequent lookups.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain **Linear Search**.
* Explain **Dictionary Lookup**.
* Label Linear Search as **O(n)**.
* Label Dictionary Lookup as **O(1) Average-Case**.
* Translate both complexity labels into plain language.
* Explain why one tiny timing result doesn't determine Big-O.
* Connect Input Size to growth.
* Use timing experiments as evidence without confusing them with Big-O.
* Choose a lookup strategy based on an actual program requirement.
* Explain the tradeoff without claiming Linear Search is always wrong.

---

# 🔓 Next Unlock

Efficient code that produces the wrong answer is still wrong.

Your final quest asks a different question:

> **The code runs. But is it actually correct?**

[**Continue to Quest 1.10 — Looks Right. Is It? (Days 18–19) →**](quest-10-debugging.md)
