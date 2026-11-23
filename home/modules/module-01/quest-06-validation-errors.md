# Quest 1.6 — Validate, Catch, Keep Going: Validation and Error Handling (Days 9–10)

**Total time:** about 60 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · **Load, save, and protect** · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Sometimes a form comes back filled in wrong. For example, a sign-up sheet asks for each person's age. One person writes "twenty." Another writes 250. A third leaves it blank. A program that trusts every line will make a wrong list, or stop partway through.

A careful program does two jobs:

* **Validation:** it checks each line against rules before using it.
* **Error handling:** it plans what to do when a step fails anyway.

In this reading, you'll learn how to:

* write one function that checks every line and returns a list of problems
* check a line's shape before you check its values
* use `try` and `except` to catch one bad line and keep going
* name the error you expect, instead of catching every error

**Main takeaway:** Validation asks, "Does this input meet our rules?" Error handling asks, "What happens if this step fails?" Use both, and never hide errors you didn't expect.

**Why it matters at work:** Real data files always have some bad lines. One bad line shouldn't stop the whole file. It also shouldn't slip through without anyone noticing.

## Learning goals

Check off each goal once you can do it.

- [ ] I can write a validation function that checks a record's shape first, then its values, and returns a list of problems.
- [ ] I can use `try` and `except` so one bad line doesn't stop a whole batch.
- [ ] I can name the error I expect, like `ValueError` or `KeyError`, and explain why a bare `except:` is risky.

**Skills:** Functions & Modular Programming · Attention to Detail

## Quick recall

* Recall that `return` hands a value back to the line that called the function. You wrote functions that return values in [Build It Once, Use It Again](quest-02-functions-scope.md). This reading's function returns a whole list.
* Recall that after a JSON round trip, `restored[7]` raised a `KeyError`, because the key had become the string `"7"`. You saw this in [Make It Survive](quest-05-serialization.md). The second reading shows how to catch an error like that.
* Recall that code that sounds sure, or runs without errors, can still be wrong. You check it against something real, as you did in [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md). Here, you'll test a function on a few made-up lines instead of trusting it.

## Words to know

### Is this line usable?: Validation

**Validation** means checking data against your rules before you use it. It answers one question: does this input meet our rules?

For example, each line in the reading's file looks like this: a student ID, a grade, and a class, with a bar between them.

```text
S-2041|10|Biology
```

| Word | What it means |
| --- | --- |
| **Record** | One full entry, like one sign-up form or one room request. |
| **Field** | One part of a record. Each sign-up line in the reading has three fields: a student ID, a grade, and a class. A bar character separates them. |
| **Batch file** | A file with one record on each line. A program checks it one line at a time. |
| **Valid input** | Input that passes every rule, so the program can safely use it. |
| **Invalid input** | Input that breaks at least one rule. It can have the right shape and still hold a wrong value, like grade 14 when only 9 to 12 is allowed. |
| **Malformed input** | Input with the wrong shape, like a line with 2 fields when 3 are required. It's one kind of invalid input. |
| **Structure check** | Checks that a record has the right shape, such as exactly 3 fields. It always runs first. |
| **Value check** | Checks what a field holds, such as "is the grade a whole number from 9 to 12?" |
| **Contract** | What a function takes in and what it gives back. The rest of the program relies on it. |

### Tools for checking a line

| Code | What it does |
| --- | --- |
| **`.split()`** | A string method. `form.split(sep)` cuts the string at every `sep` and gives back a list of the pieces. In the reading, `sep` is the bar character. Each piece is still a string. |
| **`.isdigit()`** | A string method. It gives `True` when every character is a digit. `"10".isdigit()` is `True`. `"10th".isdigit()` and `"".isdigit()` are `False`. |
| **`int(text)`** | Turns the text `"10"` into the number `10`. `int("10th")` stops the program with an error. |
| **`not`** | Flips `True` to `False`, and `False` to `True`. |
| **`or`** | Gives `True` when either side is `True`. |
| **`!=`** | Means "is not equal to." |
| **`enumerate(forms, start=1)`** | Gives a loop two things on each pass: a position number and the item. The parameter `start` is set to `1`, so the count begins at 1, not 0. |
| **f-string** | Text with an `f` in front, like `f"Line {num}"`. Python puts the value of `num` where the braces are. |

### When a step fails: Exceptions and error handling

**Error handling** means deciding, in code, what should happen when a step fails, so one failure doesn't stop the whole program.

| Word | What it means |
| --- | --- |
| **Exception** | An error Python raises while a program runs. If no code catches it, the program stops at that line. |
| **Raise** | What Python does when a step fails: it creates an exception. |
| **Traceback** | The report Python prints when no code catches an exception. Read its last line first: it names the error. |
| **`try`** | The block that holds the risky step you want Python to attempt. |
| **`except ValueError:`** | The block that runs only if a line in `try` raises a `ValueError`. It catches that error and no other. |
| **Bare `except:`** | `except:` with no error name. It catches every error, even typos and real bugs, so avoid it. |

Four errors come up again and again. Each name tells you what went wrong:

| Error | Example from the reading | What went wrong |
| --- | --- | --- |
| **`ValueError`** | `int("4 nights")` | The right operation, but this value can't be used. |
| **`KeyError`** | `rates["penthouse"]` | The dictionary has no entry for that key. |
| **`IndexError`** | `rooms[5]` when `rooms` has 3 items | The list has no item at that position. |
| **`NameError`** | `print(totl)` when only `total` exists | Python can't find that name, often because of a typo. |

## Before you read

Here's an answer: "My program checks that every line has 3 fields, so every line it accepts is good data."

Something is off about it. What? See if the reading agrees with you.

## Read

This quest has two readings. Do them in order.

### Reading 1: Trust, But Verify (Day 9)

As you read, look for:

1. Why the structure check (counting fields) has to run before any value check.
2. Why the function returns a list of problems, instead of printing them or returning `True` or `False`.
3. What goes wrong when `return problems` is indented one step too far, and how a tiny test batch catches it.

**[Start the reading: Trust, But Verify →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/first-validation-function/reading-1-trustbutverify/)** (about 24 minutes)

### Reading 2: Try It, Catch It, Keep Going (Day 10)

As you read, look for:

1. How many guests get booked before the program stops on `"4 nights"`, and what changes once you add `try` and `except`.
2. Where Python goes when a line inside `try` raises an error, and which line runs after that.
3. Why `except ValueError:` is safer than a bare `except:`.

**[Start the reading: Try It, Catch It, Keep Going →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/error-handling/reading-1-tryitcatchitkeepgoing/)** (about 22 minutes)

## Main takeaways

### Summary

* **Validation checks the rules before you use the data.** Run the structure check first (right number of fields?), then the value checks (is the grade a whole number from 9 to 12?). The right shape doesn't mean the right values.
* **Return the problems, don't just print them.** A list of problem messages can be counted, printed, or tested on a tiny batch. That's how you catch quiet bugs, like a `return` inside the loop.
* **`try` and `except` catch one failure so the batch keeps going.** Put the risky step in `try`. Name the error you expect after `except`. A bare `except:` hides real bugs.

### Validation in code

Here is the checking function from the first reading, with shorter messages:

```python
def find_form_problems(forms):
    problems = []
    for num, form in enumerate(forms, start=1):
        fields = form.split("|")
        if len(fields) != 3:
            problems.append(f"Line {num}: expected 3 fields")
        elif not fields[1].isdigit():
            problems.append(f"Line {num}: grade not a number")
        elif int(fields[1]) < 9 or int(fields[1]) > 12:
            problems.append(f"Line {num}: grade outside 9-12")
    return problems
```

**Code walkthrough:**

1. The function has one parameter, `forms`: the list of form lines, exactly as the office typed them.
2. `problems = []` starts an empty list. The function adds one message for each bad line.
3. `enumerate(forms, start=1)` gives each line a number, starting at 1, so each message can say which line failed. (The reading calls this variable `line_number`.)
4. `form.split("|")` cuts the line into its fields.
5. The structure check runs first: `len(fields) != 3`. A line with 2 fields has no grade to check, so reading `fields[2]` would stop the program with an error.
6. Then come the value checks. `.isdigit()` runs before `int()`, so `int()` only ever sees digits.
7. `return problems` sits at the same indent as `for`, so it runs once, after every line is checked. Indent it one more step and the function returns after line 1.

![A flow for one sign-up form line. Check 1, the structure check: exactly 3 fields? If no, add the problem "Line 2: expected 3 fields" for S-2042|Chemistry. If yes, check 2, a value check: is the grade all digits? If no, add "Line 3: grade '10th' is not a number." If yes, check 3, a value check: is the grade 9 to 12? If no, add "Line 4: grade 14 is outside 9-12." If yes, the line is valid and adds no message, like lines 1 and 5. Each problem goes into the list with problems.append. After the last line, the function returns problems: 3 problems found.](images/m1b-form-checks.svg)

### Error handling in code

Here is the booking program from the second reading, with the risky step inside `try`:

```python
for request in requests:
    guest, nights_text, room = request.split("|")
    try:
        nights = int(nights_text)
        print("Booked", guest, "for", nights, "nights")
    except ValueError:
        print("Skipped", guest)
```

**Code walkthrough:**

1. `requests` is the list of room requests, like `"Okafor|2|double"`.
2. `request.split("|")` cuts each request into three fields. The three names on the left each get one field, in order.
3. `int(nights_text)` is the risky step. For `"4 nights"`, it raises a `ValueError`.
4. When that happens, Python leaves `try` at that line, so `"Booked"` doesn't print. It jumps to `except ValueError:` and prints `"Skipped Batista"`.
5. Then the loop moves on to the next request. Lindqvist and Moreau still get rooms.

![A flow using read_nights.py from the reading. Step 1, try: nights = int(nights_text). Step 2: did that line raise a ValueError? For "3", no: the rest of try runs, it prints Nights: 3, and except is skipped. For "4 nights", yes: Python jumps to except ValueError, skips the rest of try, and prints Could not read: 4 nights. Step 3: both paths continue after try and except, printing Done with, and the program keeps going.](images/m1b-try-except-flow.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The line has 3 fields, so it's valid." | Shape is only the first check. Student S-2044's line has 3 fields, but its grade, 14, is outside 9 to 12. |
| "No error means the function works." | With `return problems` inside the loop, the function reports "0 problems found" and raises no error. Test it on a tiny batch. |
| "A bare `except:` is safest, because it catches everything." | It also catches typos and real bugs, and hides the traceback that would point to them. |
| "If a line in `try` fails, the rest of `try` still runs." | Python leaves `try` at that line and jumps to the matching `except`. |
| "Validation and error handling are the same thing." | Validation checks values against rules, like `if nights > 30`. Error handling responds when a step fails, like `int("4 nights")`. `int("45")` works, so only validation catches a 45-night stay. |

### How this connects

* **Next reading:** You'll write a second function that takes the checked data and sums it up, such as a total and a count. You'll decide what that function's one job is, and what it should leave to other functions.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Your program will check each record against clear rules and report every problem with its line number. It will keep going when one record can't be read.

## Quick check

**1.** Which one catches each problem: validation or error handling?

* A. A form says the grade is 14, but only 9 to 12 is allowed.
* B. `int("ten")` would stop the program.

<details>
<summary>Answer</summary>

A is **validation**: the value breaks a rule, but no step fails. B is **error handling**: `int("ten")` raises a `ValueError`, so you wrap it in `try` and catch it with `except ValueError:`.

</details>

**2.** What does this code print?

```python
prices = {"tea": 3, "cake": 5}
try:
    print(prices["coffee"])
    print("Found it")
except KeyError:
    print("Not on the menu")
print("Next order")
```

<details>
<summary>Answer</summary>

```text
Not on the menu
Next order
```

`prices["coffee"]` raises a `KeyError`, so Python leaves `try` at that line. `"Found it"` never prints. The `except` block runs, and then the program keeps going.

</details>

---

**Next:** [Quest 1.7 — One Job at a Time: Writing a Second Function (Days 11–12)](quest-07-second-function.md)
