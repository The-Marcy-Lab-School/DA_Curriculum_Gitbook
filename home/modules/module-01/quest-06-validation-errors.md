# Quest 1.6 — Validate, Catch, Keep Going: Validation and Error Handling (Days 9–10)

**Total time:** About 65 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · **Load, save, and protect** · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Introduction

Sometimes a form comes back filled in wrong. For example, a sign-up sheet asks for each person's age. One person writes "twenty." Another writes 250. A third leaves it blank. A program that trusts every line will make a wrong list, or stop partway through. In the picture below, look at the three red lines on the left sheet.

![Two sign-up sheets with five ages each. Left, some ages break the rules: lines 1 and 5 are grey, 34 and 27. Three lines are red: line 2 says "twenty", which is not a number; line 3 says 250, which is too big for an age; line 4 is left blank. A program that trusts every line stops at "twenty", or keeps 250. Right, every age passes the checks: five grey ages, 34, 19, 52, 41, and 27. Each age is a whole number a person could be, so the program can use all 5.](images/signup-ages-bad-entries.svg)

A careful program does two jobs:

* **Validation:** it checks each line against rules before using it.
* **Error handling:** it plans what to do when a step fails anyway.

**Main takeaway:** Use validation to catch data that breaks your rules, and error handling to keep going when a step fails. **Validation** means checking data against your rules before you use it. **Error handling** means deciding, in code, what happens when a step fails. Name the error you expect, so you never hide errors you didn't expect.

**Why it matters at work:** Analysts check every data file before they use it, because real files always have some bad lines. For example, they use validation and error handling to:

* find sign-up forms with a missing or impossible age
* skip one unreadable line in a file of orders, and keep going
* report every bad line with its line number, so someone can fix it

If you skip these checks, one bad line can stop the whole file, or slip into your totals without anyone noticing.

## Learning goals

After this reading, you should be able to say:

* I can write a validation function that checks a record's shape first, then its values, and returns a list of problems.
* I can use `try` and `except` so one bad line doesn't stop a whole batch.
* I can name the error I expect, like `ValueError` or `KeyError`, and explain why a bare `except:` is risky.

**Skills:** Functions & Modular Programming · Attention to Detail

## Quick recall

* In [Build It Once, Use It Again](quest-02-functions-scope.md), `return` handed a value back to the line that called the function. This reading's function returns a whole list.
* When you loaded a dictionary back from a JSON (JavaScript Object Notation) file in [Make It Survive](quest-05-serialization.md), `restored[7]` raised a `KeyError`. The key had become the string `"7"`, and the second reading shows how to catch an error like that.
* Code can sound sure, or run without errors, and still be wrong. Module 0's [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md) taught you to check it against something real. Here, you'll test a function on a few made-up lines instead of trusting it.

## Words to know

### Is this line usable?: Validation

**Validation** means checking data against your rules before you use it. It answers one question: does this input meet our rules?

For example, each line in the reading's file looks like this: a student ID, a grade, and a class, with a bar between them. Here, the **grade** is the student's year in school, from 9 to 12.

```text
S-2041|10|Biology
```

The examples come from the reading's 5 sign-up lines, for students S-2041 to S-2045.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Record** | One full entry, like one sign-up form or one hotel room request. | Student S-2041's line: ID, grade 10, and Biology |
| **Field** | One part of a record. Each sign-up line in the reading has three fields: a student ID, a grade, and a class. A bar character separates them. | `"10"`, the grade in S-2041's line |
| **Batch file** | A file with one record on each line. A program checks it one line at a time. | The office's file of 5 sign-up lines |
| **Valid input** | Input that passes every rule, so the program can safely use it. | S-2041's line: 3 fields, and grade 10 |
| **Invalid input** | Input that breaks at least one rule. It can have the right shape and still hold a wrong value. | S-2044's line: 3 fields, but grade 14 |
| **Malformed input** | Input with the wrong shape. It's one kind of invalid input. | S-2042's line has 2 fields: an ID and `Chemistry`. |
| **Structure check** | Checks that a record has the right shape, such as exactly 3 fields. It always runs first. | `len(fields) != 3` |
| **Value check** | Checks what a field holds, such as "is the grade a whole number from 9 to 12?" | `"10th".isdigit()` gives `False`. |
| **Contract** | What a function takes in and what it gives back. The rest of the program relies on it. | Takes a list of lines. Gives back a list of problem messages. |

You've met records before. In [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), one line of `pets.csv` was one pet's record, with commas between its values. Here, one line is one student's record, and a bar separates its fields.

### Tools for checking a line

| Code | What it does |
| --- | --- |
| **`.split()`** | A string method. `form.split(sep)` cuts the string at every `sep` and gives back a list of the pieces. In the reading, `sep` is the bar character. Each piece is still a string. |
| **`.isdigit()`** | A string method. It gives `True` when every character is a digit. `"10".isdigit()` is `True`. `"10th".isdigit()` and `"".isdigit()` are `False`. |
| **`int(text)`** | Turns the text `"10"` into the number `10`. `int("10th")` stops the program with an error. |
| **`not`** | Flips `True` to `False`, and `False` to `True`. `not "10th".isdigit()` is `True`. |
| **`or`** | Gives `True` when either side is `True`. For grade 14, `14 < 9 or 14 > 12` is `True`. |
| **`!=`** | Means "is not equal to." For S-2042's line, `2 != 3` is `True`. |
| **`enumerate(forms, start=1)`** | Gives a loop two things on each pass: a position number and the item. The parameter `start` is set to `1`, so the count begins at 1, not 0. |
| **f-string** | Text with an `f` in front, like `f"Line {num}"`. Python puts the value of `num` where the braces are. |

Each piece from `.split()` is text, even `"10"`. Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md) showed that digits in quotes are text. An ID stays text, because it's a label. So the code turns the grade into a number with `int()`, to compare it with 9 and 12. The student ID `S-2041` stays text.

### When a step fails: Exceptions and error handling

**Error handling** means deciding, in code, what should happen when a step fails, so one failure doesn't stop the whole program.

The examples come from the second reading's hotel booking program. One guest, Batista, asked for `"4 nights"` instead of a number.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Exception** | An error Python raises while a program runs. If no code catches it, the program stops at that line. | A `ValueError` |
| **Raise** | What Python does when a step fails: it creates an exception. | `int("4 nights")` raises a `ValueError`. |
| **Traceback** | The report Python prints when no code catches an exception. Read its last line first: it names the error. | Last line: `ValueError: invalid literal for int() with base 10: '4 nights'` |
| **`try`** | The block that holds the risky step you want Python to attempt. | `nights = int(nights_text)`, inside `try:` |
| **`except ValueError:`** | The block that runs only if a line in `try` raises a `ValueError`. It catches that error and no other. | It prints `Skipped Batista`. |
| **Bare `except:`** | `except:` with no error name. It catches every error, even typos (typing mistakes) and real bugs (mistakes in code), so avoid it. | It would also hide `print(totl)`, a typo for `total`. |

Four errors come up again and again. Each name tells you what went wrong:

| Error | Example in the reading | What went wrong |
| --- | --- | --- |
| **`ValueError`** | `int("4 nights")` | The right operation, but this value can't be used. |
| **`KeyError`** | `rates["penthouse"]` | The dictionary has no entry for that key. (`rates` holds room prices. A penthouse is a room on the top floor.) |
| **`IndexError`** | `rooms[5]` when `rooms` has 3 items | The list has no item at that position. |
| **`NameError`** | `print(totl)` when only `total` exists | Python can't find that name, often because of a typo. |

## Before you read

Here's an answer: "My program checks that every line has 3 fields, so every line it accepts is good data."

Something is off about it. What? See if the reading agrees with you.

## ⭐ Read

This quest has two readings. Do them in order.

### Reading 1: Trust, But Verify (Day 9)

As you read, look for:

1. Why the structure check (counting fields) has to run before any value check.
2. Why the function returns a list of problems, instead of printing them or returning `True` or `False`.
3. What goes wrong when `return problems` is indented one step too far, and how a tiny test batch catches it.

**[Start the reading: Trust, But Verify →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/first-validation-function/reading-1-trustbutverify/)** (about 24 minutes)

### Reading 2: Try It, Catch It, Keep Going (Day 10)

As you read, look for:

1. How many guests get booked (given a hotel room) before the program stops on `"4 nights"`, and what changes once you add `try` and `except`.
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

<details>
<summary>Expand to walk through the code</summary>

1. The function has one parameter, `forms`: the list of form lines, exactly as the office typed them.
2. `problems = []` starts an empty list. The function adds one message for each bad line.
3. `enumerate(forms, start=1)` gives each line a number, starting at 1, so each message can say which line failed. (The reading calls this variable `line_number`.)
4. `form.split("|")` cuts the line into its fields.
5. The structure check runs first: `len(fields) != 3`. A line with 2 fields has no grade to check, so reading `fields[2]` would stop the program with an error.
6. Then come the value checks. `.isdigit()` runs before `int()`, so `int()` only ever sees digits.
7. `return problems` sits at the same indent as `for`, so it runs once, after every line is checked. Indent it one more step and the function returns after line 1.

</details>

The picture below follows one line through the three checks, in order. Look at where each of the reading's bad lines stops.

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

<details>
<summary>Expand to walk through the code</summary>

1. `requests` is the list of room requests, like `"Okafor|2|double"`: a guest's name, the number of nights, and the room type.
2. `request.split("|")` cuts each request into three fields. The three names on the left each get one field, in order.
3. `int(nights_text)` is the risky step. For `"4 nights"`, it raises a `ValueError`.
4. When that happens, Python leaves `try` at that line, so `"Booked"` doesn't print. It jumps to `except ValueError:` and prints `"Skipped Batista"`.
5. Then the loop moves on to the next request. Lindqvist and Moreau still get rooms.

</details>

The picture below uses a shorter program from the reading, `read_nights.py`. Follow the two inputs, `"3"` and `"4 nights"`, down their two paths.

![A flow using read_nights.py from the reading. Step 1, try: nights = int(nights_text). Step 2: did that line raise a ValueError? For "3", no: the rest of try runs, it prints Nights: 3, and except is skipped. For "4 nights", yes: Python jumps to except ValueError, skips the rest of try, and prints Could not read: 4 nights. Step 3: both paths continue after try and except, printing Done with, and the program keeps going.](images/m1b-try-except-flow.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The line has 3 fields, so it's valid." | Shape is only the first check. Student S-2044's line has 3 fields, but its grade, 14, is outside 9 to 12. |
| "My function ran with no error, so it works." | With `return problems` inside the loop, it reports "0 problems found" for the 5 lines. The right answer is 3. Test it on a tiny batch. |
| "A bare `except:` is the safest choice, because it catches everything." | It also catches typos. Type `totl` instead of `total`, and a bare `except:` hides the `NameError` that would point to it. |
| "When `int()` fails, the `print` line under it in `try` still runs." | Python leaves `try` at the line that failed. For Batista, `Booked` never prints. `Skipped Batista` prints instead. |
| "Validation and error handling are two names for the same thing." | Validation checks values against rules, like `if nights > 30`. Error handling responds when a step fails, like `int("4 nights")`. `int("45")` works, so only validation catches a 45-night stay. |

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
