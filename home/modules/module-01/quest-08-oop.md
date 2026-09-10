## Quest 1.8 — Meet the Objects (Days 13–15)

### 🎯 Your Mission

Functions help organize behavior.

Data Structures help organize collections.

Now you'll learn another way to organize a program: **Object-Oriented Programming (OOP)**.

A Class lets you define a blueprint for a kind of thing. From that blueprint, you can create multiple independent Objects that share a common structure and behavior.

**Target:** Define a Class, create independent Objects, and explain the roles of `__init__`, `__str__`, and `__repr__`.

---

## 🔑 Vocabulary Mission

Be ready to recognize and explain:

* **Object-Oriented Programming (OOP)**
* **Class**
* **Object**
* **Instance**
* **Attribute**
* **Method**
* `self`
* `__init__`
* `__str__`
* `__repr__`

Keep this relationship in mind:

**Class → Blueprint**

**Object / Instance → One specific thing created from that blueprint**

---

## 🎮 Warm-Up: One Blueprint, Two Items

Imagine your Inventory Tracker needs to represent:

```text
Item A
Name: Laptop
Quantity: 4
Category: Electronics
```

and:

```text
Item B
Name: Camera
Quantity: 9
Category: Electronics
```

Both are Items.

But they're not the **same** Item.

If both Objects come from the same Class, should changing Item A's Quantity automatically change Item B's Quantity?

Why or why not?

Lock in your prediction.

---

# 🎯 Main Mission — REQUIRED

Days 13–14 have **two required readings**.

Day 15 is your independent Class-design rep.

Complete both readings before moving to the solo challenge.

---

## 🏗️ Part 1 — Meet the Objects — Day 13

**Lecture Connection:** OOP: Building a Class With a Partner

Your first mission is to understand the relationship between a Class and the Objects created from it.

[**Start Required Reading: Meet the Objects →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/oop-buildingaclass/reading-1-meettheobjects/)

As you read, hunt for:

* What a Class represents.
* What an Object or Instance represents.
* How Attributes store information about an Object.
* How Methods define behavior.
* What `self` refers to.
* How multiple Objects created from one Class remain independent.

When you return, be ready to answer:

> **What's the difference between a Class and an Object?**

---

## ✨ Part 2 — Two Ways to Introduce an Object — Day 14

**Lecture Connection:** Magic Methods — `__init__` / `__str__` / `__repr__`

Now focus on the special Methods Python can use when Objects are created and represented.

[**Start Required Reading: Two Ways to Introduce an Object →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/magic-methods/reading-1-twowaystointroduceanobject/)

As you read, hunt for:

* When `__init__` runs.
* How `__init__` establishes an Object's initial Attributes.
* What `__str__` controls.
* What `__repr__` is meant to communicate.
* Why useful Object representations can make debugging easier.

When you return, be ready to explain:

> **Why might the way an Object represents itself matter while you're debugging or inspecting a program?**

---

# ⚡ Checkpoint 1: Class or Object?

Consider:

```python
class Item:
    pass

laptop = Item()
camera = Item()
```

Identify:

**The Class**

**Object 1**

**Object 2**

### First Attempt

Answer before opening the Hint.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Which thing defines the blueprint?

Which things were created from it?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The **Class** is:

```python
Item
```

The two **Objects / Instances** are:

```python
laptop
camera
```

Both Objects were created from the same `Item` Class, but they are independent instances.

</details>

---

# ⚡ Checkpoint 2: What Is `self`?

Consider:

```python
class Item:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity
```

In:

```python
self.quantity
```

what does `self` refer to?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Imagine creating:

```python
laptop = Item("Laptop", 4)
camera = Item("Camera", 9)
```

Whose Quantity should `self.quantity` refer to during each Object's initialization?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

`self` refers to the **current instance** the Method is working with.

When initializing `laptop`, `self.quantity` belongs to the `laptop` Object.

When initializing `camera`, `self.quantity` belongs to the `camera` Object.

That's how different Objects created from the same Class can maintain their own instance Attributes.

</details>

---

# 🐛 Misconception Check: When Does `__init__` Run?

A teammate says:

> “`__init__` runs every time I use an Object.”

Correct or incorrect?

### First Attempt

Explain what event actually triggers `__init__`.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think about the moment you write:

```python
item = Item(...)
```

Is the Object being created—or merely used again later?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The statement is **incorrect**.

`__init__` runs as part of initializing a new instance when that Object is created.

It does not rerun every time you later access an Attribute or call another Method on the Object.

Think:

**Create New Object → `__init__`**

not:

**Use Existing Object → `__init__` Again**

</details>

---

# 🔍 Object Independence Check

Consider:

```python
laptop = Item("Laptop", 4)
camera = Item("Camera", 9)

laptop.quantity = 2
```

What should `camera.quantity` still be?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

The Objects share a Class.

Do they share the same instance Attributes?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

`camera.quantity` should still be:

```text
9
```

`laptop` and `camera` are independent Objects.

Changing an instance Attribute on `laptop` does not automatically change the corresponding Attribute on `camera`.

This independence is essential for your Inventory Tracker.

</details>

---

# ✨ Magic Method Match

Match each Method with its main role.

### `__init__`

### `__str__`

### `__repr__`

Choices:

**A.** Establish an Object's initial state when the instance is created.

**B.** Provide a readable string representation of the Object.

**C.** Provide a representation useful for understanding or inspecting the Object.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Retrieve the role of each Method rather than focusing only on its spelling.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A useful match is:

**`__init__` → A**

Establishes the initial state of a new Object.

**`__str__` → B**

Provides a readable string representation.

**`__repr__` → C**

Provides a representation intended to help describe or inspect the Object.

The important distinction is that these Methods have different responsibilities.

</details>

---

# 🧪 Solo Class Design — Day 15

**Lab Connection:** Solo Class Design Rep

The partner scaffolding is gone.

Design an `Item` Class that could support your future Inventory Tracker.

Your Class needs to represent:

* A Name.
* A Quantity.
* A Category.

It also needs behavior that can determine whether the Item is **low-stock**.

## Step 1 — Design Before Syntax

Complete:

```text
Class:
Item

Attributes:
- ?
- ?
- ?

Behavior:
- ?
```

Ask:

**What information belongs to each Item?**

**What behavior belongs to an Item?**

---

## Step 2 — Build Independently

Create the Class without copying a finished solution.

Then create at least **two different Objects**.

For example, your Objects should be able to represent two Items with different Names and Quantities.

---

## Step 3 — Test Independence

Change the Quantity of one Object.

Verify that the other Object does **not** change.

Don't assume.

Run the test.

---

## Step 4 — Inspect Your Objects

Try your Object representations.

Ask:

* What happens when I print the Object?
* Is the output useful to a person?
* What representation would help me while debugging?

Connect those questions to `__str__` and `__repr__`.

---

# 🐛 Bug Hunt: Undefined Attribute

Consider:

```python
class Item:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def describe(self):
        return f"{self.name}: {self.category}"
```

The programmer creates:

```python
laptop = Item("Laptop", 4)
```

Then calls:

```python
laptop.describe()
```

What's the problem?

### First Attempt

Trace the Attributes created during `__init__`.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Which Attributes exist?

```text
name
quantity
category
```

Were all three created?

</details>

### Second Attempt

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

The Method tries to access:

```python
self.category
```

but `category` was never created on the Object.

`__init__` created only:

```python
self.name
self.quantity
```

This is an **Undefined Attribute** problem.

One fix would be to make `category` part of the Object's initialization if every Item is expected to have one.

The key debugging habit is to compare:

**Attribute Used → Attribute Actually Created**

</details>

---

# 🧠 OOP or Just Functions?

A teammate says:

> “Now that we know Classes, every program should use OOP.”

Do you agree?

Explain your reasoning.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think back to your single-purpose Functions.

Does learning a new tool mean every problem requires that tool?

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

No.

A Class can be useful when you need multiple independent instances that share a common structure and related behavior.

But a short program may be clearer with simple Data Structures and Functions.

The goal isn't:

> **“Use OOP everywhere.”**

The goal is:

> **“Choose an organization that fits the problem.”**

</details>

---

# 💼 Interview Arena

> **When might you choose a Class instead of only using Functions and loose data?**

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Think:

**Multiple Instances → Related Data → Related Behavior**

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

I might use a Class when I need to represent multiple independent instances of the same kind of thing and keep their related data and behavior together.

For example, an Inventory Tracker may have many Item Objects that each have their own Name, Quantity, and Category while sharing behaviors defined by the `Item` Class.

I wouldn't automatically use a Class for every program. I'd use it when that organization makes the problem clearer.

</details>

---

# 🏁 Final Check

You're ready to move on when you can:

* Explain **Class** versus **Object / Instance**.
* Identify Attributes and Methods.
* Explain what `self` refers to.
* Explain when `__init__` runs.
* Explain the basic roles of `__str__` and `__repr__`.
* Create multiple independent Objects from one Class.
* Verify that changing one Object doesn't automatically change another.
* Recognize an Undefined Attribute problem.
* Design a simple Class independently.
* Explain when a Class may be useful without claiming every program needs OOP.

---

# 🔓 Next Unlock

You now have Objects that can represent individual inventory Items.

But your inventory may eventually contain thousands of them.

Remember your Day 6 question:

> **What happens as the collection grows?**

Now you're ready to compare two real lookup strategies.

[**Continue to Quest 1.9 — Lookups Matter (Days 16–17) →**](quest-09-big-o-practice.md)
