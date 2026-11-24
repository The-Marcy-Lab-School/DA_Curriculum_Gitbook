# Quest 1.5 — Make It Survive: Saving Data to Files (Day 8)

**Total time:** About 40 minutes

**Building blocks:** Decide and repeat · Organize steps · Hold data · **Load, save, and protect** · Check your work ([what's this?](introduction.md#the-big-picture-the-building-blocks-of-a-data-program))

## Quick recall

* In [Pick the Right Container](quest-04-data-structures.md), you used a **dictionary** to store key/value pairs. A **tuple** is an ordered record (a group of values about one thing) that can't change. In this reading, you'll save a dictionary whose values are tuples, and see what comes back.
* `ls` lists the files in a folder, from Module 0's [Meet Your Terminal](../module-00/quest-01-terminal.md). `cat pets.csv` printed what's inside a file, in the interactive reading for Module 0's [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md). You'll use both to look inside the file your program saves.

## Introduction

Sometimes your work disappears when a program stops. For example, you type a long shopping list into a phone app. The app crashes (stops suddenly) before it saves. When you open it again, the list is gone. It lived only in the app's memory, not in a file.

Python programs work the same way. When a program stops, every variable is gone. To keep data, the program must write it to a file. Later, a program can read the file and build the data again.

**Main takeaway:** Saving data to a file and loading it back can change its types. **Serialization** means turning a Python value into text you can save in a file. When JSON loads that text back, the key `7` comes back as the string `"7"`. A tuple comes back as a list.

**Why it matters at work:** Analysts save and load data files every day, so later runs and teammates can use the data. For example, they use files to:

* save a program's results, like each hour's rain, so the next run can use them
* load data that another program sent, often as JSON
* keep a **log**: a file that gets one new line each time something happens

If a key or a number comes back as a different type, the program gives wrong answers with no error message.

## Learning goals

After this reading, you should be able to say:

* I can open a file to write, add to, or read it, and pick the right mode: `"w"`, `"a"`, or no mode.
* I can save a dictionary with `json.dump` and load it back with `json.load`.
* I can name what changes on a JSON round trip and check the type of each loaded value.

**Skills:** Attention to Detail

## New Python module: json

**What it's for:** `json` saves a Python value as JSON text in a file, and builds a Python value again from that text. Each job takes one line.

`json` is a **module**: one file of Python code that you load with `import`. It comes with Python, so there's nothing to install.

**JSON** (JavaScript Object Notation) is a text format for saving data. JSON text looks a lot like a Python dictionary, but it isn't one:

* A Python dictionary lives in memory while the program runs: `{6: (0.4, 58)}`.
* JSON text lives in a file after the program stops: `{"6": [0.4, 58]}`. Its keys are always in double quotes, and it has square brackets where Python had a tuple.

**How you'll see it in this reading:**

```python
# save_rain.py
import json  # load the module
rain = {6: (0.4, 58), 7: (1.2, 55)}
with open("rain.json", "w") as f:
    json.dump(rain, f)

# load_rain.py, run later
import json
with open("rain.json") as f:
    rain = json.load(f)
print(rain["7"])  # [1.2, 55]
```

<details>
<summary>Expand to walk through the code</summary>

1. `import json` loads the `json` module. It goes at the top of each file that uses it. After it, you can use `json.dump` and `json.load`.
2. `rain` is a dictionary. Each key is an hour of the day. Each value is a tuple: the rain in millimeters, then the temperature in degrees Fahrenheit.
3. `with open("rain.json", "w") as f:` opens the file `rain.json` for writing and gives it the short name `f`.
4. `json.dump(rain, f)` is a function in the `json` module. It turns `rain` into JSON text and writes it into the open file `f`. This is **serialization**, or saving.
5. In a later run, `open("rain.json")` opens the same file. There's no mode, so it opens the file for reading.
6. `json.load(f)` reads the JSON text and builds a brand-new dictionary from it. This is **deserialization**, or loading.
7. `rain["7"]` uses the string `"7"`, not the number `7`, because JSON keys are always strings. It gives back `[1.2, 55]`: a list, not the tuple you saved.

</details>

You may see `json.dumps` and `json.loads` in other examples. The extra *s* stands for *string*: they work with a string instead of a file.

**Learn more:** [Python docs: json](https://docs.python.org/3/library/json.html) (official) · [Python docs: Reading and Writing Files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files) (official) · [W3Schools: Python JSON](https://www.w3schools.com/python/python_json.asp) · [W3Schools: Python File Handling](https://www.w3schools.com/python/python_file_handling.asp)

## Words to know

### Keeping data after the program stops: Serialization

The examples come from the reading's weather program.

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Memory** | Where a running program keeps its variables. Everything in memory is gone when the program stops. | `rain` is gone when `save_rain.py` stops. |
| **Serialization** | Turning a Python value into text that can be saved to a file. Its everyday name is *saving*. | `json.dump(rain, f)` writes `rain` into `rain.json`. |
| **Deserialization** | Building a Python value again from saved text. Its everyday name is *loading*. | `json.load(f)` builds `rain` again in `load_rain.py`. |
| **Round trip** | Saving a value and then loading it back. Compare what comes back with what you saved. | Save `{6: (0.4, 58)}`. Load back `{"6": [0.4, 58]}`. |
| **Format** | The rules for how data is laid out as text in a file. The format decides how the data reads back. | JSON, CSV, or TXT |

### Which kind of file?: JSON, CSV, and TXT

For example, here is one hour's reading saved in each of the three formats:

```text
JSON:  {"hour": 7, "rain_mm": 1.2}

CSV:   hour,rain_mm
       7,1.2

TXT:   7:00 rain 1.2 mm
```

| Format | What it holds | Use it for |
| --- | --- | --- |
| **JSON** | Data with structure inside it. A JSON **object** looks like a Python dictionary. A JSON **array** looks like a Python list. | One record that holds a list or another record inside it |
| **CSV** | Short for "comma-separated values." A table. The column names come once, in a **header row**. Then each line is one row, with commas between the values. | A table someone will open in a spreadsheet |
| **TXT** | Short for "text." Plain text with no built-in structure. Your program decides the layout. | A simple log (a file that gets one new line each time something happens) that only your own program writes and reads |

You've opened a CSV file before. In [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md), `pets.csv` had the column names on its first line. Each line after it was one pet's record. Now your own program can write a file like that.

JSON text has three rules that Python dictionaries don't follow. Check them when you read a JSON file by hand, for example one an AI (artificial intelligence) assistant wrote. That's the habit from [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md): check what an AI gives you before you trust it. The three rules:

* Strings and keys use double quotes: `"roof"`, never `'roof'`.
* `true`, `false`, and `null` are lowercase. Python's `True`, `False`, and `None` aren't valid JSON.
* There's no comma after the last item.

### Opening a file: open() and modes

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **`open(name, mode)`** | A built-in function that finds a file, or makes it, so your code can write to it or read it. | `open("rain_note.txt", "w")` |
| **Mode** | The second argument you give `open()`. It says what you plan to do with the file. | `"w"`, `"a"`, or no mode |
| **`"w"` (write)** | Empties the file first, then writes. If the file doesn't exist, Python makes it. | 3 hourly runs with `"w"` leave 1 line: `8:00 rain 0.9 mm`. |
| **`"a"` (append)** | Keeps what's already in the file and adds to the end. *Append* means "add to the end." | 3 hourly runs with `"a"` leave all 3 lines. |
| **No mode, or `"r"` (read)** | Opens the file for reading. | `open("rain.json")` |
| **`with open(...) as f:`** | Opens a file and names it `f` for the indented lines below. When those lines end, Python closes the file for you. | `with open("rain_note.txt", "w") as f:` |
| **`f.write(text)`** | A method that adds the text to the open file. | `f.write("6:00 rain 0.4 mm\n")` |
| **`f.read()`** | A method that gives back everything in the file as one string. | After two writes, it gives both lines as one string. |
| **`"\n"`** | Inside a string, it means "start a new line here." Without it, the next write lands on the same line. | Without it, you get `6:00 rain 0.4 mm7:00 rain 1.2 mm`. |
| **`FileNotFoundError`** | The error Python raises when you try to read a file that doesn't exist yet. | Running `load_rain.py` before `save_rain.py` has made `rain.json` |

The mode matters most when a program adds one line at a time. For example, the reading's weather program adds a line to its log every hour. In the picture below, compare the top row, opened with `"w"`, with the bottom row, opened with `"a"`.

![Two rows of file snapshots after the 6:00, 7:00, and 8:00 runs. Top row, opened with "w" (write), which empties the file first every run: the file holds only 6:00 rain 0.4 mm, then only 7:00 rain 1.2 mm, then only 8:00 rain 0.9 mm. Bottom row, opened with "a" (append), which adds to the end: the file grows from one line to two lines to all three lines. Note: use "a" for a log. With "w", only the last hour is left.](images/m1b-write-vs-append.svg)

### What comes back different: Types after loading

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Data type** | What kind of value something is: a string (`str`), a whole number (`int`), a decimal number (`float`), a tuple, a list, or a dictionary. | `58` is an `int`. `0.4` is a `float`. |
| **Keys become strings** | JSON keys are always strings. | The integer key `6` comes back as the string `"6"`. |
| **Tuples become lists** | JSON has no tuple type. | The tuple `(0.4, 58)` comes back as the list `[0.4, 58]`. |
| **Text files give back strings** | Every value read from a text file is a string, even text that looks like a number. Turn it into a number before you do math with it. | You get `"1.5"`, not `1.5`. |
| **`KeyError`** | The error Python raises when a dictionary has no entry for the key you asked for. | `restored[7]` after the round trip, when the key is now `"7"` |
| **"not JSON serializable"** | A `TypeError` that means JSON has no way to store that type of value. | `json.dump` on a record that holds a calendar date |
| **`datetime`** | A module that comes with Python for calendar dates. In the reading, `from datetime import date` loads it. | `date(2026, 10, 3)` stores October 3, 2026. |

The picture below follows `rain` on a round trip, from Python to a file and back. Look at the two notes about what came back different.

![Three panels. In Python while the program runs: rain = {6: (0.4, 58), 7: (1.2, 55)}, with integer keys and tuple values. An arrow labeled json.dump(), save, leads to rain.json on disk: {"6": [0.4, 58], "7": [1.2, 55]}, with string keys and lists. An arrow labeled json.load(), load, leads back to Python later, where the keys are still strings and the values are still lists. Two notes: the integer 6 came back as the string "6", so rain[6] now raises a KeyError. The tuple (0.4, 58) came back as the list [0.4, 58], because JSON has no tuples.](images/m1b-json-round-trip.svg)

{% hint style="info" %}
**Check the type of every loaded value.** Nothing crashes when a type changes on the way. The program just gives wrong answers later.
{% endhint %}

## Before you read

In the reading, you'll focus on a school's rooftop weather station: tools on the roof that measure rain and temperature. A Python program keeps each hour's rain in a dictionary, like `{6: (0.4, 58), 7: (1.2, 55)}`.

Think about: if you save this dictionary to a file and load it back tomorrow, will you get exactly the same dictionary? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. Why the hourly log keeps only one line, and the one-letter fix.
2. What `print(restored[7])` does after a JSON round trip, and why.
3. What happens when you try to save a calendar date with `json.dump`.

**[Start the reading: Make It Survive →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod1/data-serialization/reading-1-makeitsurvive/)** (about 24 minutes)

## Main takeaways

### Summary

* **A file holds text, not live Python values.** Saving (serialization) writes a text version. Loading (deserialization) builds a brand-new value from that text.
* **Pick the mode on purpose.** `"w"` starts the file fresh, `"a"` adds to the end, and no mode reads it. Opening a log with `"w"` erases every earlier line.
* **Check types after loading.** JSON turns integer keys into strings and tuples into lists. Text files give back strings. Pick the format that fits the data: JSON for records with lists inside, CSV for flat tables, TXT for simple logs.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The file holds my dictionary." | It holds text: `{"6": [0.4, 58], "7": [1.2, 55]}`. Loading builds a new dictionary from that text, and it can differ from the one you saved. |
| "It loaded with no error, so it's the same data." | The key `7` came back as `"7"`, and `(1.2, 55)` came back as `[1.2, 55]`. Neither change shows an error. |
| "`"w"` adds a line to my file." | `"w"` empties the file first. After 3 hourly runs with `"w"`, the log holds only `8:00 rain 0.9 mm`. Use `"a"`. |
| "The file says 1.5, so I get the number 1.5 back." | You get the string `"1.5"`. Turn it into a number with `float("1.5")` first. |
| "JSON and CSV are both text files, so they work the same." | They lay data out differently. A day's alerts, like `["wind", "storm"]`, fit inside a JSON record, but not in one flat CSV cell. |
| "Python's `True` is fine in a JSON file." | JSON writes it as lowercase `true`. A file with `True` in it isn't valid JSON. |

### How this connects

* **Next reading:** Data that comes from a file is often messy. You'll write a function that checks each line against rules before the program uses it, and lists every problem it finds. Then you'll keep a program running when one line can't be read.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Your program will save its data to a file and load it back. You'll check that each value came back with the type you expect.

## Quick check

**1.** A loop runs 5 times. Each time, it opens `log.txt` with `"w"` and writes one line. How many lines are in the file at the end?

<details>
<summary>Answer</summary>

One. Each `"w"` empties the file first, so only the last line is left. Use `"a"` to keep all 5 lines.

</details>

**2.** You save `{1: "Mon", 2: "Tue"}` with `json.dump`, then load it back into `days`. What happens when you run `days[1]`?

<details>
<summary>Answer</summary>

Python raises a `KeyError`. JSON keys are always strings, so the keys are now `"1"` and `"2"`. Use `days["1"]`.

</details>

---

**Next:** [Quest 1.6 — Validate, Catch, Keep Going: Validation and Error Handling (Days 9–10)](quest-06-validation-errors.md)
