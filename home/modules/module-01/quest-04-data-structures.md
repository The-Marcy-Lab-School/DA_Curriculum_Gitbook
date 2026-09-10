## Quest 1.4 — Pick the Right Container (Day 7)

### 🎯 Your Mission

Programs don't just work with individual values.

They organize **collections of values**, and the way you organize that data affects what your program can easily do with it.

Today, you'll compare Python's core Data Structures and practice choosing a container based on the job.

**Target:** Recognize common Python Data Structures, explain their key characteristics, and choose a structure based on what your program needs to do.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Data Structure**
* **List**
* **Tuple**
* **Dictionary**
* **Set**
* **Key**
* **Value**
* **Mutable**
* **Immutable**

Don't treat these as four disconnected vocabulary words.

Ask:

> **What does this structure let my program represent or do?**

---

## 🎮 Warm-Up: Pick the Relationship

Imagine you're building an inventory system.

You want to connect each Item Name to its Quantity:

```text id="6zywew"
"laptop" → 8
"charger" → 14
"camera" → 3
```

Which feature sounds especially useful?

**A.** Store each value only by its position.

**B.** Associate a unique Key with a Value.

Lock in your prediction.

More importantly, explain **why** that feature matches the job.

---

# 🎯 Main Mission — REQUIRED

## 📦 Pick the Right Container — Day 7

**Lecture Connection:** Python Data Structures

Your goal isn't to memorize isolated syntax.

Your goal is to understand the choices Python gives you for organizing collections.

[**Start Required Reading: Pick the Right Container →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/python-data-structures/reading1-pickrightcontainer/)

As you read, hunt for the differences between:

**List · Tuple · Dictionary · Set**

Pay attention to:

* How each structure organizes values.
* How you access its contents.
* Whether it is Mutable or Immutable.
* What makes Dictionary Keys useful.
* What makes Sets different from Lists.
* What kind of task might make one structure a better fit than another.

When you return, be ready to answer:

> **Why isn't there one Python Data Structure that's automatically best for every problem?**

---

# ⚡ Checkpoint 1: Key → Value

You want to represent:

```text id="o2yflk"
"laptop" → 8
"charger" → 14
"camera" → 3
```

Which Data Structure naturally represents these **Key → Value** relationships?

**A.** List

**B.** Dictionary

### First Attempt

Choose one and explain the relationship you're trying to represent.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Which Python Data Structure stores Values under Keys?

</details>

### Second Attempt

Try again before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B. Dictionary**

A Dictionary stores **Key–Value pairs**.

For example:

```python id="d29zwr"
inventory = {
    "laptop": 8,
    "charger": 14,
    "camera": 3
}
```

Here, the Item Names are Keys and the Quantities are Values.

The important point isn't just the syntax.

The structure matches the relationship the program needs to represent.

</details>

---

# ⚡ Checkpoint 2: List or Set?

You have:

```python id="vm2fzq"
categories = ["electronics", "books", "electronics", "supplies"]
```

For a particular task, you care only about the **unique category names**.

Which structure could help represent that requirement?

**A.** List

**B.** Set

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Do you need repeated values for this particular task?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B. Set**

A Set represents a collection of unique values.

For this task, repeated `"electronics"` entries aren't necessary because the question asks only which unique categories exist.

That doesn't mean Sets are always better than Lists.

It means the Set matches **this requirement**.

</details>

---

# 🔒 Mutable or Immutable?

Consider two questions:

**1. Will this collection need to change after I create it?**

**2. Should this collection stay fixed?**

Why might those questions matter when choosing between Data Structures?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Retrieve these two terms:

**Mutable**

**Immutable**

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A **Mutable** structure can be changed after it is created.

An **Immutable** structure cannot be changed in the same way after creation.

Whether your collection is supposed to change can therefore be part of choosing an appropriate Data Structure.

The goal isn't:

> “Mutable is better.”

The goal is:

> **“Which behavior fits the data and the task?”**

</details>

---

# 🎮 Container Match

Match each need to the Data Structure that seems most appropriate.

### Need 1

You need an ordered collection that your program will update.

### Need 2

You need Key–Value relationships.

### Need 3

You care about unique values.

### Need 4

You need a fixed collection that should not be modified after creation.

Your choices:

* **List**
* **Tuple**
* **Dictionary**
* **Set**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Ask what makes each structure distinct.

Don't choose based on which syntax you remember most easily.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A reasonable match is:

**Need 1 → List**

Lists are ordered and Mutable.

**Need 2 → Dictionary**

Dictionaries represent Key–Value relationships.

**Need 3 → Set**

Sets represent unique values.

**Need 4 → Tuple**

Tuples are Immutable and can represent a collection that should remain fixed.

Real programming decisions can involve additional tradeoffs, but these characteristics give you a starting point for choosing deliberately.

</details>

---

# 🔁 Big-O Callback

Remember Day 6?

You predicted what might happen when a collection becomes much larger.

Now you have another piece of the puzzle:

**The Data Structure you choose can affect how your program accesses information.**

Don't solve the entire performance question yet.

Save this prediction:

> **If I frequently need to retrieve an Item using its unique name, how might a Dictionary help?**

You'll test that reasoning during **Days 16–17**.

---

# 💼 Interview Arena

> **How do you decide which Python Data Structure to use?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Don't answer:

> “Whichever one is fastest.”

Start with:

**What does the program need to store and do?**

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

I start by identifying what the program needs to represent and which operations matter.

For example, if I need an ordered collection that will change, a List may fit. If I need Key–Value relationships and want to retrieve information using a unique Key, a Dictionary may be a better fit.

I choose the Data Structure based on the requirements rather than assuming one structure is always best.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain what a **Data Structure** is.
* Recognize a List, Tuple, Dictionary, and Set.
* Explain **Key → Value** relationships.
* Explain Mutable versus Immutable.
* Identify a structure that represents unique values.
* Choose a Data Structure based on a stated requirement.
* Defend your choice instead of only naming the structure.
* Connect Data Structure choice back to the Big-O question from Day 6.

---

# 🔓 Next Unlock

Your Python program can organize information while it's running.

But what if that information needs to **leave the running program, be saved, or be used somewhere else?**

Next: make the data survive.

[**Continue to Quest 1.5 — Make It Survive (Day 8) →**](quest-05-serialization.md)
