# Quest 1.8 — Meet the Objects: Classes and Objects (Days 13–15)

**Total time:** about 55 minutes

**Building blocks:** Decide and repeat · Organize steps · **Hold data** · Load, save, and protect · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Many things in a program come in sets of the same kind. For example, a gym uses one sign-up form for every member. The form has the same blanks each time: name, plan, and visits this month. Each member fills in their own copy. Ana's visits never change Jay's.

In Python, the blank form is a **class**. Each filled-in copy is an **object**.

In this reading, you'll learn how to:

* write a class that stores each object's starting values
* make several objects from one class, and keep their values apart
* write a method that works on one object's own values
* choose what an object shows when you print it

**Main takeaway:** A class describes one kind of thing, once. Each object made from it keeps its own values.

**Why it matters at work:** Data programs handle many records of the same kind. A class keeps each record's values together, and apart from every other record. Many Python packages for data are built from classes, so these words will come up again and again.

## Learning goals

Check off each goal once you can do it.

- [ ] I can write a class with `__init__`, make two objects from it, and show that changing one doesn't change the other.
- [ ] I can tell an attribute from a method, and say what `self` means inside a method.
- [ ] I can add `__str__` and `__repr__` to a class, and predict which one `print()`, `repr()`, and a list will use.

**Skills:** Object-Oriented Programming

## Quick recall

* Recall that a **parameter** is a name in a function's `def` line, and an **argument** is the value you pass in when you call it, from [Build It Once, Use It Again](quest-02-functions-scope.md). A class has a function inside it with parameters, too.
* Recall that a dictionary stores values under labels called keys, like `goal["saved_amount"]`, from [Pick the Right Container](quest-04-data-structures.md). A class also groups labeled values. It adds the actions that use them.
* Recall the **f-string** from [Build It Once, Use It Again](quest-02-functions-scope.md): `f"Hi, {name}!"` fills in the value of `name`. The second reading builds strings this way.

## Words to know

### What is a class?: Classes and objects

| Word | What it means |
| --- | --- |
| **Class** | A description of one kind of thing: what each one stores (attributes) and what it can do (methods). You write it once and make many objects from it. |
| **Object** | One specific thing made from a class, with its own values. |
| **Instance** | Another word for object. "`goal_a` is an instance of `SavingsGoal`" means `goal_a` was made from that class. |
| **Object-Oriented Programming (OOP)** | A way of writing programs around objects. Each object holds its data and the actions that use that data. |
| **CapWords** | The naming style for classes. Each word starts with a capital letter, with no spaces or underscores: `SavingsGoal`. Variables, functions, and methods use lowercase words joined by underscores: `saved_amount`. Both rules come from PEP 8, Python's style guide. See [the Module 1 Introduction](introduction.md#python-syntax-and-style). |

### What is inside an object?: Attributes, methods, and self

| Word | What it means |
| --- | --- |
| **Attribute** | A value stored on an object. You read it with a dot and no parentheses: `goal_a.name`. |
| **Method** | A function written inside a class. You call it with a dot and parentheses: `goal_a.is_funded()`. The parentheses mean "run this method." |
| **`__init__`** | The setup method. Python runs it by itself, once, each time a new object is made. It stores the incoming values as that object's attributes. |
| **`self`** | Inside a method, the object the method is working on: the object before the dot. Python passes it in for you. |
| **Dunder** | Short for "double underscore." `__init__` is said "dunder init." |

For example, this is the class from the first reading:

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

**Code walkthrough:**

1. `class SavingsGoal:` starts the class. Everything indented under it belongs to the class.
2. `def __init__(self, name, target_amount, saved_amount):` is the setup method. `self` is the new object. The other three parameters receive the values you pass in.
3. `self.name = name` stores the value of the parameter `name` on this object, as an attribute called `name`. The next two lines do the same for the other values.
4. `def is_funded(self):` is a method. It reads this object's own attributes and returns `True` or `False`.
5. `SavingsGoal("Bike Fund", 500, 420)` makes a new object, and Python runs `__init__` once. The parameter `name` is set to `"Bike Fund"`, `target_amount` is set to `500`, and `saved_amount` is set to `420`. You never pass `self` yourself.

### How does an object describe itself?: Magic methods

| Word | What it means |
| --- | --- |
| **Magic method** | A method whose name starts and ends with two underscores, like `__init__`, `__str__`, or `__repr__`. Python calls it for you at the right moment. Also called a dunder method. |
| **`__str__`** | Returns a friendly string for a person to read. `print(obj)`, `str(obj)`, and `f"{obj}"` use it. |
| **`__repr__`** | Returns an exact string for programmers, usually shaped like the code that made the object, such as `Pet('Biscuit', 'dog')`. `repr(obj)` and lists use it. |
| **Default representation** | What Python shows when a class has neither method: the class name plus a memory address, like `<__main__.Pet object at 0x7f2b1c0a4d90>`. |
| **Memory address** | Where an object is stored in the computer's memory. It changes each time you run the file, so it doesn't tell you which object you have. |

## Before you read

In the first reading, you'll focus on a budgeting app that saves for several goals at once, like a Bike Fund and a Trip Fund. Both goals are made from the same class.

Think about: you add money to the Bike Fund. Should the Trip Fund's saved amount change too? Why or why not? Write down your first answer, then see if the reading agrees.

## Read

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

![On the left, the SavingsGoal class lists three attributes, name, target_amount, and saved_amount, and one method, is_funded(). It creates two objects. goal_a holds Bike Fund, 500, and 420. goal_b holds Trip Fund, 1200, and 1200. goal_a.is_funded() runs with self as goal_a, checks 420 >= 500, and returns False. goal_b.is_funded() runs with self as goal_b, checks 1200 >= 1200, and returns True. A note says changing goal_a.saved_amount to 480 changes only goal_a.](images/m1c-class-objects.svg)

One class makes two objects. The same method gives different answers, because `self` points to a different object each time.

![A decision tree that starts with the question: what is asking Python to describe the object? print, str, or an f-string asks for the friendly view. If the class has __str__, Python shows Biscuit the dog. If not, it falls back to __repr__ and shows Pet('Biscuit', 'dog'). repr, or an object inside a list, always uses __repr__, so a list prints [Pet('Biscuit', 'dog'), Pet('Mochi', 'cat')]. With neither method, Python shows the class name and a memory address.](images/m1c-str-repr.svg)

To predict the output, ask what is asking Python to describe the object.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`__init__` runs every time I use an object." | It runs once, when the object is made. Reading an attribute or calling a method doesn't run it again. |
| "Two objects from the same class share their values." | Each object stores its own attributes. Changing one object leaves the others alone. |
| "I pass `self` when I make an object." | Python passes `self` for you. Write `SavingsGoal("Bike Fund", 500, 420)`, not `SavingsGoal(self, "Bike Fund", 500, 420)`. |
| "`__str__` should print the string." | It must **return** the string. `print()` then shows what it returns. |
| "A list of objects uses `__str__`." | A list shows each item with `__repr__`, even when the class has a `__str__`. |

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
