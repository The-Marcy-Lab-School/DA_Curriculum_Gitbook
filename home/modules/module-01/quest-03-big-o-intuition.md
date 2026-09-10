## Quest 1.3 — When the Crowd Grows (Day 6)

### 🎯 Your Mission

Two approaches can both feel fast when you're working with five items.

That doesn't mean they'll behave the same way with five thousand—or five million.

Today you're building your first intuition for **Big-O**.

You do **not** need to become a complexity theorist.

You do need to start asking:

> **What happens to the amount of work as the input gets bigger?**

**Target:** Explain in plain language how the amount of work an approach requires can change as Input Size grows.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Input Size**
* **Algorithm**
* **Linear Scan**
* **Lookup**
* **Big-O**
* **Scale**

Keep this distinction in mind:

**Runtime Measurement → What happened during this run?**

**Big-O → How does the work grow as the input grows?**

---

## 🎮 Warm-Up: The Growing List

Imagine searching for a student's name by checking a list from the beginning:

```text
1. Check the first name.
2. Is it the name I need?
3. If not, check the next name.
4. Repeat until found.
```

Now imagine the name you're looking for is last.

### Scenario A

The list contains **10 names**.

### Scenario B

The list contains **10,000 names**.

Without calculating an exact runtime:

**Which scenario could require more checks?**

Then answer the more important question:

> **What changed about the amount of work when the input got larger?**

Lock in your reasoning before the reading.

---

# 🎯 Main Mission — REQUIRED

## 📈 When the Crowd Grows — Day 6

**Lecture Connection:** Big-O Intuition — Why Some Lookups Stay Fast

This reading introduces the mental model you'll use throughout the rest of the module.

As you read, hunt for:

* What **Input Size** means.
* Why we care about growth instead of only one runtime.
* What happens during a Linear Scan.
* How Big-O helps describe scalability.
* Why two approaches that seem similar on tiny inputs can behave differently as the data grows.

[**Start Required Reading: When the Crowd Grows →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/big-o-intuition/reading-1-whenthecrowdgrows/)

When you return, be ready to explain:

> **What question is Big-O trying to help you answer?**

---

# ⚡ Checkpoint 1: Stopwatch or Growth?

Which question is Big-O trying to help answer?

**A.** “Exactly how many milliseconds did this code take on my laptop?”

**B.** “How does the amount of work change as the Input Size grows?”

### First Attempt

Choose one and explain your reasoning.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

A stopwatch measures one execution under particular conditions.

Big-O focuses on a pattern of **growth**.

</details>

### Second Attempt

Try again before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B.**

Big-O helps describe how the amount of work grows as Input Size grows.

A specific timing measurement can still be useful, but it's answering a different question.

Think:

**Timing → This Run**

**Big-O → Growth Pattern**

</details>

---

# 🔎 Checkpoint 2: Linear Scan

Imagine a collection:

```python
items = ["camera", "laptop", "charger", "tablet", "monitor"]
```

You search from the beginning until you find `"monitor"`.

How many items do you inspect?

Now imagine the collection contains **500 items** and the target is still last.

What changed?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

In a Linear Scan, you're checking items one at a time.

What happens when there are more items before the target?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

In the five-item example, you inspect all **5 items** before reaching `"monitor"`.

If the collection contains 500 items and the target is last, you may need to inspect all **500 items**.

As the collection grows, the amount of work required by the Linear Scan can grow with it.

That's the important intuition.

</details>

---

# 🧠 Scale Challenge

A teammate says:

> “My search took almost no time when I tested it on five items, so performance isn't something we need to think about.”

What's missing from that reasoning?

### First Attempt

Respond in one or two sentences.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Five items tell you something about five items.

What happens if the real collection becomes much larger?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

Testing five items tells you how the approach behaved on a very small input.

It doesn't tell you how the amount of work will grow as the collection becomes much larger.

That's why reasoning about **Scale** matters.

</details>

---

# 🔮 Prediction: Save This Answer

You'll return to Big-O later in the module.

For now, imagine two inventory systems.

### System A

To find `"camera"`, the program checks Items one by one until the names match.

### System B

To find `"camera"`, the program uses `"camera"` as a Dictionary Key.

Which approach do you predict will be more affected as the inventory becomes much larger?

Write your prediction.

**Don't worry about proving it yet.**

You'll revisit this prediction during Days 16–17 when you compare **Linear Search** with **Dictionary Lookup**.

---

# 💼 Interview Arena

> **What does Big-O tell you that a single timing measurement doesn't?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Use this phrase:

**“As the Input Size grows…”**

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

A timing measurement tells me how long one execution took under particular conditions.

Big-O helps me reason about how the amount of work grows as the Input Size grows.

That makes it useful for thinking about how an approach may scale beyond the small example I'm testing right now.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain **Input Size**.
* Explain Big-O in plain language.
* Distinguish growth from one stopwatch measurement.
* Explain what happens during a Linear Scan.
* Explain why a Linear Scan may require more work as a collection grows.
* Use **Scale** when reasoning about an approach.
* Ask, **“What happens as the input gets bigger?”**

You don't need to memorize a long table of Big-O notation yet.

The goal today is the mental model.

---

# 🔓 Next Unlock

Now you know that **how you access data can matter as the data grows**.

Next, you'll investigate the different containers Python gives you for organizing that data.

[**Continue to Quest 1.4 — Pick the Right Container (Day 7) →**](quest-04-data-structures.md)
