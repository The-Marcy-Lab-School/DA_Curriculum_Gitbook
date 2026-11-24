# Quest 1.8 — Meet the Objects: Classes and Objects (Days 13–15)

**Total time:** About 60 minutes

**Building blocks:** Decide and repeat · Organize steps · **Hold data** · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Many things in a program come in sets of the same kind. For example, a gym uses one sign-up form for every member. The form has the same blanks each time: name, plan (the type of membership the person pays for), and visits this month. Each member fills in their own copy. Ana's visits never change Jay's.

In Python, the blank form is a **class**. Each filled-in copy is an **object**.

**Main takeaway:** A **class** describes one kind of thing, once. Each **object** made from it keeps its own values. For example, `goal_a` and `goal_b` both come from the `SavingsGoal` class. Changing `goal_a`'s saved amount from 420 to 480 doesn't change `goal_b`.

**Why it matters at work:** Analysts use classes to keep each record's values together, and apart from every other record. A **record** is the data about one thing, like one gym member. For example, classes help them:

* store each gym member's name, plan, and visits in one object
* give every record the same actions, like checking whether a savings goal is funded
* read code from Python packages for data, which are built from classes

Without a class, ten savings goals need 30 separate variables, like `name_2` and `saved_2`, and they're easy to mix up.

## Learning goals

After this reading, you should be able to say:

* I can write a class with `__init__`, make two objects from it, and show that changing one doesn't change the other.
* I can tell an attribute from a method, and say what `self` means inside a method.
* I can add `__str__` and `__repr__` to a class, and predict which one `print()`, `repr()`, and a list will use.

**Skills:** Object-Oriented Programming

## Quick recall

* In Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), every pet in `pets.csv` had the same columns, like name, age, and weight. A **record** is one row about one thing, and a **column** is one kind of information every record has.
* Your dictionaries in [Pick the Right Container](quest-04-data-structures.md) stored values under labels called keys, like `goal["saved_amount"]` in this reading. A class also groups labeled values, and it adds the actions that use them.
* [Build It Once, Use It Again](quest-02-functions-scope.md) taught **parameters**, the names in a `def` line, and **arguments**, the values you pass in. It also taught the **f-string**: `f"Cost: ${saved}"` fills in the value of `saved`. A class has a function inside it with parameters, and the second reading builds f-strings.

## Words to know

### What is a class?: Classes and objects

The examples come from the first reading's budgeting app.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Class** | A description of one kind of thing: what each one stores (attributes) and what it can do (methods). You write it once and make many objects from it. | `SavingsGoal` |
| **Object** | One specific thing made from a class, with its own values. | `goal_a`, which holds Bike Fund, 500, and 420 |
| **Instance** | Another word for object. | "`goal_a` is an instance of `SavingsGoal`" means `goal_a` was made from that class. |
| **Object-Oriented Programming (OOP)** | A way of writing programs around objects. Each object holds its data and the actions that use that data. | Each goal holds its own amounts and its own `is_funded()` check. |
| **CapWords** | The naming style for classes. Each word starts with a capital letter, with no spaces or underscores. Variables, functions, and methods use lowercase words joined by underscores instead. Both rules come from PEP 8 (PEP stands for "Python Enhancement Proposal"), Python's style guide. See [the Module 1 Introduction](introduction.md#python-syntax-and-style). | `SavingsGoal` (a class), but `saved_amount` (a variable) |

A class works like the column names at the top of `pets.csv`. It lists the same blanks once. Each object is one record that fills in those blanks with its own values.

### What is inside an object?: Attributes, methods, and self

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Attribute** | A value stored on an object. You read it with a dot and no parentheses. | `goal_a.name` gives `"Bike Fund"`. |
| **Method** | A function written inside a class. You call it with a dot and parentheses. The parentheses mean "run this method." | `goal_a.is_funded()` gives `False`. |
| **`__init__`** | The setup method. Python runs it by itself, once, each time a new object is made. It stores the incoming values as that object's attributes. | It runs once when `SavingsGoal("Bike Fund", 500, 420)` runs. |
| **`self`** | Inside a method, the object the method is working on: the object before the dot. Python passes it in for you. | In `goal_b.is_funded()`, `self` is `goal_b`. |
| **Dunder** | Short for "double underscore." | `__init__` is said "dunder init." |

You've already called methods, like `stops.append("Oak Rd")` in [Pick the Right Container](quest-04-data-structures.md). Now you'll write your own.

An object is a lot like a dictionary that also has its own actions. Compare a goal stored each way, from the reading:

| | Dictionary | Object |
| --- | --- | --- |
| **Read one value** | `goal["saved_amount"]` gives `300` | `goal_a.saved_amount` gives `420` |
| **Run an action** | No `is_funded()`. You'd write a separate function. | `goal_a.is_funded()` gives `False` |
| **Same labels every time** | Each dictionary can have different keys. | Every `SavingsGoal` object gets the same three attributes. |

For example, this is the class from the first reading. It describes a **savings goal**: an amount of money you want to save for one thing, like a bike.

```python
class SavingsGoal:  # CapWords name
    def __init__(self, name, target_amount, saved_amount):
        self.name = name
        self.target_amount = target_amount
        self.saved_amount = saved_amount

    def is_funded(self):
        return self.saved_amount >= self.target_amount

goal_a = SavingsGoal("Bike Fund", 500, 420)
```

<details>
<summary>Expand to walk through the code</summary>

1. `class SavingsGoal:` starts the class. Everything indented under it belongs to the class.
2. `def __init__(self, name, target_amount, saved_amount):` is the setup method. `self` is the new object. The other three parameters receive the values you pass in.
3. `self.name = name` stores the value of the parameter `name` on this object, as an attribute called `name`. The next two lines do the same for the other values.
4. `def is_funded(self):` is a method. It reads this object's own attributes and returns `True` or `False`. A goal is **funded** when the saved amount has reached the target amount.
5. `SavingsGoal("Bike Fund", 500, 420)` makes a new object, and Python runs `__init__` once. The parameter `name` is set to `"Bike Fund"`, `target_amount` is set to `500`, and `saved_amount` is set to `420`. You never pass `self` yourself.

</details>

### How does an object describe itself?: Magic methods

The examples come from the second reading's pet-sitting app, where `biscuit = Pet("Biscuit", "dog")`.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Magic method** | A method whose name starts and ends with two underscores. Python calls it for you at the right moment. Also called a dunder method. | `__init__`, `__str__`, or `__repr__` |
| **`__str__`** | Returns a friendly string for a person to read. `print(obj)`, `str(obj)`, and `f"{obj}"` use it. | `print(biscuit)` shows `Biscuit the dog`. |
| **`__repr__`** | Returns an exact string for programmers, usually shaped like the code that made the object. `repr(obj)` and lists use it. | `repr(biscuit)` gives `Pet('Biscuit', 'dog')`. |
| **Default representation** | What Python shows when a class has neither method: the class name plus a memory address. | `<__main__.Pet object at 0x7f2b1c0a4d90>` |
| **Memory address** | Where an object is stored in the computer's memory. It changes each time you run the file, so it doesn't tell you which object you have. | `0x7f2b1c0a4d90` |

## Before you read

In the first reading, you'll focus on a budgeting app: an app that helps you plan how to spend and save money. It saves for several goals at once, like a Bike Fund and a Trip Fund. A **fund** is money you save for one purpose. Both goals are made from the same class.

Think about: you add money to the Bike Fund. Should the Trip Fund's saved amount change too? Why or why not? Write down your first answer, then see if the reading agrees.

## ⭐ Read

There are two readings. Do them in order.

As you read the first one, look for:

1. The four steps Python takes when `goal_a = SavingsGoal("Bike Fund", 500, 420)` runs.
2. What `self` is when you call `goal_a.is_funded()`, and what it is when you call `goal_b.is_funded()`.
3. What happens to `goal_b` when `goal_a`'s saved amount changes.

**[Start the reading: Meet the Objects →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/oop-buildingaclass/reading-1-meettheobjects/)** (about 23 minutes)

As you read the second one, look for:

1. What Python shows when you print an object whose class has no `__str__` and no `__repr__`.
2. Who each method is written for: people, or programmers.
3. The question you ask to predict which method Python uses, and what a list does.

**[Start the reading: Two Ways to Introduce an Object →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/magic-methods/reading-1-twowaystointroduceanobject/)** (about 24 minutes)

## Main takeaways

### Summary

* **Write the class once. Each object keeps its own values.** `__init__` runs once for each new object and stores its starting values on `self`. Changing `goal_a.saved_amount` leaves `goal_b` alone.
* **An attribute is a stored value. A method is a function inside the class.** Read an attribute with no parentheses. Call a method with parentheses. When a method runs, `self` is the object before the dot.
* **`__str__` is for people. `__repr__` is for programmers.** `print()` uses `__str__`, and falls back to `__repr__` when there is no `__str__`. `repr()` and lists always use `__repr__`. If you write only one, write `__repr__`.

The picture below shows one class making two objects. Follow `is_funded()` for `goal_a`, then for `goal_b`.

![On the left, the SavingsGoal class lists three attributes, name, target_amount, and saved_amount, and one method, is_funded(). It creates two objects. goal_a holds Bike Fund, 500, and 420. goal_b holds Trip Fund, 1200, and 1200. goal_a.is_funded() runs with self as goal_a, checks 420 >= 500, and returns False. goal_b.is_funded() runs with self as goal_b, checks 1200 >= 1200, and returns True. A note says changing goal_a.saved_amount to 480 changes only goal_a.](images/m1c-class-objects.svg)

The same method gives different answers, because `self` points to a different object each time.

To predict what Python shows, ask what is asking Python to describe the object. The decision tree below starts with that question. Follow the branch for `print()`, then the branch for a list.

![A decision tree that starts with the question: what is asking Python to describe the object? print, str, or an f-string asks for the friendly view. If the class has __str__, Python shows Biscuit the dog. If not, it falls back to __repr__ and shows Pet('Biscuit', 'dog'). repr, or an object inside a list, always uses __repr__, so a list prints [Pet('Biscuit', 'dog'), Pet('Mochi', 'cat')]. With neither method, Python shows the class name and a memory address.](images/m1c-str-repr.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`__init__` runs every time I use an object." | It runs once, when the object is made. `goal_a.name` and `goal_a.is_funded()` don't run it again. |
| "`goal_a` and `goal_b` come from the same class, so they share their values." | Each object stores its own attributes. Change `goal_a.saved_amount` to 480, and `goal_b.saved_amount` stays 1200. |
| "I have to pass `self` when I make an object." | Python passes `self` for you. Write `SavingsGoal("Bike Fund", 500, 420)`, not `SavingsGoal(self, "Bike Fund", 500, 420)`. |
| "`__str__` should print the string." | It must **return** the string, like `return f"{self.name} the {self.species}"`. `print()` then shows `Biscuit the dog`. |
| "My class has a `__str__`, so a list of pets will use it." | A list shows each item with `__repr__`: `[Pet('Biscuit', 'dog'), Pet('Mochi', 'cat')]`. |

### How this connects

* **Next reading:** You'll go back to finding things in a collection. You'll compare checking items one at a time with jumping straight to an item by its key, and see how the gap grows as the data grows.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll design a small class for the records your program keeps track of. You'll choose its attributes and methods, and show that two objects don't affect each other.

## Quick check

**1.** What does this code print? Name the class, the objects, and one attribute.

```python
class Pet:
    def __init__(self, name, species):
        self.name = name
        self.species = species

biscuit = Pet("Biscuit", "dog")
mochi = Pet("Mochi", "cat")
mochi.name = "Miso"
print(biscuit.name)
```

<details>
<summary>Answer</summary>

It prints `Biscuit`. `Pet` is the class. `biscuit` and `mochi` are objects. `name` and `species` are attributes. Changing `mochi.name` doesn't touch `biscuit`.

</details>

**2.** The `Pet` class has the reading's `__repr__` method but no `__str__`. What does `print(biscuit)` show? What does `print([biscuit])` show?

<details>
<summary>Answer</summary>

`Pet('Biscuit', 'dog')`, then `[Pet('Biscuit', 'dog')]`. With no `__str__`, `print()` falls back to `__repr__`. A list always uses `__repr__`.

</details>

---

**Next:** [Quest 1.9 — Lookups Matter: Search Speed in Practice (Days 16–17)](quest-09-big-o-practice.md)
