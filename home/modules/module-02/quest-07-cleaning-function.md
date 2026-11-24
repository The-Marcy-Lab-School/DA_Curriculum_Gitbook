# Quest 2.7 — Write It Once: Cleaning Functions (Day 8)

**Total time:** about 30 minutes

**EDA workflow:** Inspect → **Clean** → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Some data problems happen again and again. For example, every Monday a gym's sign-up sheet lists one person twice and spells "Yoga" three different ways. Fixing this by hand every week is slow, and one day you'll forget a step.

In this reading, you'll learn how to fix three common problems:

* repeated rows
* numbers saved as text
* labels spelled more than one way

You'll also learn how to put all the fixes into one function that you can run on every new file.

**Main takeaway:** Write your cleaning steps once, in a function. Prove it's reusable by running it on more than one table.

**Why it matters at work:** New data arrives every week or every month, usually with the same problems. A cleaning function fixes them the same way every time. When a fix needs to change, you change it in one place.

## Learning goals

After this reading, you should be able to say:

* I can stack two tables and remove repeated records (rows about the same real thing) using a key column.
* I can turn text into numbers and tidy up labels, then count what changed.
* I can write a cleaning function and prove it's reusable by calling it on two different inputs.

**Skills:** Data Cleaning & Imputation · Functions & Modular Programming (from Module 1)

## Quick recall

* Recall that you found repeated rows with `df.duplicated()` and number columns stored as text (`str`) in [Look Before You Filter](quest-02-inspect-filter.md). Then you chose to drop, fill, or flag each gap in [Drop, Fill, or Flag](quest-06-missing-data.md).
* Recall that `.strip()` removes spaces from both ends of a string, and `.lower()` makes every letter lowercase. You used them in Python to tidy text before you compared it: `" Peru ".strip().lower()` gives `"peru"`. In this reading, they run on a whole column.
* Recall that you wrote a validation function that checked each record against rules, in [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md), and gave each function one job, in [One Job at a Time](../module-01/quest-07-second-function.md). A cleaning function uses both ideas.

## Words to know

### Problems in a file

| Word | What it means |
| --- | --- |
| **Stack** | Put one table under another, so their rows end up in one table. |
| **Duplicate row** | The same real-world record showing up more than once, often after stacking two lists that overlap. |
| **Key column** | A column whose value names one record, like a delivery's `delivery_id`. |
| **Number stored as text** | A column of numbers that pandas loaded as text (`str`), because at least one value, like `"TBD"` (short for "to be determined"), isn't a number. Math on it gives errors or wrong answers. |
| **Label** | A value in a category column, like a country name. `"Kenya"`, `"kenya "`, and `" Kenya"` are three different labels to pandas. |

### Stacking and repeats

| Code | What it does |
| --- | --- |
| **`pd.concat([may, june], ignore_index=True)`** | Stacks the two tables, top to bottom. Setting the parameter `ignore_index` to `True` numbers the rows from 0 again, so no row label shows up twice. |
| **`.duplicated(subset="delivery_id")`** | Marks a row True when it repeats an earlier row. Setting the parameter `subset` to `"delivery_id"` means: compare only the `delivery_id` column, even if other columns differ. |
| **`.drop_duplicates(subset="delivery_id")`** | Removes the repeats, and keeps the first copy of each ID. |

### Text into numbers

| Code | What it does |
| --- | --- |
| **`pd.to_numeric(...)`** | Turns a column of text into numbers. On its own, it stops with a `ValueError` at the first value that isn't a number. |
| **Coerce** | Force a change. Setting the parameter `errors` to `"coerce"` means a value that can't become a number becomes NaN ("not a number," pandas' mark for a blank) instead of stopping with an error. |

### Tidying labels

| Code | What it does |
| --- | --- |
| **`.str`** | Lets a column use the string methods you already know. `.str.lower()` runs `.lower()` on every value in the column. |
| **`.strip()`** | Removes spaces from the start and end of text: `" Kenya"` becomes `"Kenya"`. |
| **`.lower()`** | Makes every letter lowercase: `"PERU"` becomes `"peru"`. |
| **`.value_counts()`** | Counts how many rows hold each different value in a column. Good for spotting one label spelled more than one way. |

### Functions

| Word | What it means |
| --- | --- |
| **Helper function** | A small one-job function that another function calls, like `tidy_text` inside `clean_deliveries`. |
| **Reusable function** | A function called two or more times on different inputs. A one-time script wrapped in `def` and called once isn't reusable yet. |
| **`assert`** | Stops the notebook with an error if its condition is False. A quick self-test. |

## Before you read

In the reading, you'll focus on Terra Bean, a small coffee shop that gets a list of bean deliveries every month. The May list and the June list have 5 rows each. June repeats two May deliveries, spells Kenya three ways, and says "TBD" where one bag count should be.

Think about: after you stack the two lists into one table, how many rows will it have, and how many real deliveries? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Why `.duplicated()` with no arguments finds 0 repeats when there are really 2.
2. What `errors="coerce"` does to the value `"TBD"`, and what you should count right after.
3. Why the first line of the cleaning function keeps the original table safe.

**[Start the reading: Write It Once →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/cleaning-function/reading-1-write-it-once/)** (about 20 minutes)

## Main takeaways

### Summary

* **Remove repeats by the key column, not the whole row.** A record sent twice can come back with a changed field, like a new spelling or a corrected count. Stack the lists with `pd.concat(..., ignore_index=True)`, then use `.drop_duplicates(subset="delivery_id")`.
* **Coerce, then count.** `pd.to_numeric(..., errors="coerce")` turns bad values into NaN. Count the new blanks right away, because `.mean()` skips NaN without warning you. Tidy labels with `.str.strip().str.lower()`, and check `.value_counts()` before and after.
* **Put the fixes in one function.** Its first line should make a new table, so the table you pass in stays unchanged. Call it on at least two different inputs to prove it's reusable.

![The May list has 5 rows and the June list has 5. Stacked, they make 10 rows. The function clean_deliveries runs three steps in order: remove repeats by delivery_id, turn bags into numbers, and tidy the country labels. The result is a clean table of 8 deliveries. The same function can run again on the next file.](images/cleaning-pipeline.svg)

```python
def to_number(series):
    return pd.to_numeric(series, errors="coerce")

def tidy_text(series):
    return series.str.strip().str.lower()

def clean_deliveries(df):
    df = df.drop_duplicates(subset="delivery_id")
    df["bags"] = to_number(df["bags"])
    df["country"] = tidy_text(df["country"])
    return df

clean_both = clean_deliveries(both)
clean_june = clean_deliveries(june)
```

<details>
<summary>Expand to walk through the code</summary>

1. `to_number` turns a column into numbers. The parameter `errors` is set to `"coerce"`, which means: when a value can't become a number, like `"TBD"`, make it blank (NaN) instead of stopping with an error.
2. `tidy_text` removes extra spaces with `.str.strip()` and makes every letter lowercase with `.str.lower()`, so `"Kenya "` and `"kenya"` match.
3. `clean_deliveries` runs every fix in order. Its first line removes repeated deliveries. The parameter `subset` is set to `"delivery_id"`, which means: compare only the `delivery_id` column when looking for repeats.
4. The last two lines call the same function on two different tables. That's what proves it's reusable.

</details>

{% hint style="info" %}
**Why the first line matters:** `df.drop_duplicates(...)` makes a new table, and `df =` points the name at it. If the function set a column on `df` right away instead, your original table would change too, and pandas 3 doesn't stop that.
{% endhint %}

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`.duplicated()` finds every repeat." | With no `subset=`, it only finds rows that match in *every* column. Match on the key. |
| "`errors="coerce"` fixes a bad value like 'TBD'." | It turns it into a new blank. Then you decide: drop, fill, or flag. |
| "`.str.lower()` is enough to match labels." | Spaces still split them: "kenya " and " kenya" stay different. Strip first, then lowercase. |
| "Wrapping code in `def` makes it reusable." | It's reusable once you've called it on two or more different inputs. |

### How this connects

* **Next reading:** A clean table is where analysis starts. You'll take an average that looks like a clear answer, split it by two columns at once, and check what each group is made of, so you can tell a real pattern from a misleading total.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll clean a real dataset with your own reusable cleaning function, called on more than one input, instead of copying and pasting the same fixes.

## Quick check

**1.** July's list arrives. It repeats one June delivery, says "TBD" for two counts, and has " Peru" with a space. What do you do?

<details>
<summary>Answer</summary>

Stack it with the earlier lists and run the same cleaning function, unchanged. Then check the row count and count the blanks in `bags`.

</details>

**2.** When should repeated code become a function?

<details>
<summary>Answer</summary>

At the second real repeat, or right away when the same cleaning needs to run on every new file.

</details>

---

**Next:** [Quest 2.8 — Beneath the Total: Finding Patterns in Groups (Day 9)](quest-08-mining-a-pattern.md)
