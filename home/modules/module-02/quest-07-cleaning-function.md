# Quest 2.7 — Write It Once (Day 8)

{% hint style="info" %}
**In one sentence:** Fix the common problems in a file, then put those fixes in one function you can run on every new file.
{% endhint %}

## Why this matters

Data arrives again and again: every week, every month. It often comes with the same problems: repeated rows, numbers stored as text, and one label spelled three ways. Fixing it by hand each time is slow, and it's easy to miss a step. A cleaning function does it the same way every time, and employers look for it.

## What you'll be able to do

* I can stack two files and remove repeated records using a key column.
* I can turn text into numbers and tidy up labels, then count what changed.
* I can write a cleaning function and prove it's reusable by calling it on two different inputs.

**Skills:** Data Cleaning & Imputation · Functions & Modular Programming (from Module 1)

## Words to know

| Word | What it means |
| --- | --- |
| **Duplicate row** | The same real-world record showing up more than once, often after stacking two files that overlap. |
| **Key column** | A column whose value names one record, like `delivery_id`. |
| **`pd.concat`** | Stacks tables top to bottom. |
| **Coerce** | Force a change. With `errors="coerce"`, a value that can't become a number becomes NaN instead of causing an error. |
| **`.value_counts()`** | Counts each different value in a column. Good for spotting labels spelled more than one way. |
| **Reusable function** | A function you call on two or more different inputs. |
| **`assert`** | Stops the notebook with an error if its condition is False. A quick self-test. |

## Before you read

A coffee shop's June delivery list says "Kenya," "kenya ," and " Kenya." How many countries will a count show?

<details>
<summary>Answer</summary>

Three, one for each spelling, even though they're all the same country. Extra spaces and capital letters make pandas treat them as different labels.

</details>

## Read

**[Start the reading: Write It Once →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/cleaning-function/reading-1-write-it-once/)** (about 19 minutes)

As you read, look for:

1. Why `.duplicated()` with no settings finds 0 repeats when there are really 2.
2. What `errors="coerce"` does to the value "TBD," and what you should count right after.
3. Why the first line of the cleaning function keeps the original table safe.

## Main takeaways

### Summary

* **Remove repeats by the key column, not the whole row.** A record sent twice can come back with a changed field. Stack files with `pd.concat(..., ignore_index=True)`, then use `drop_duplicates(subset="id")`.
* **Coerce, then count.** `pd.to_numeric(..., errors="coerce")` turns bad values into NaN. Count the new blanks right away, because `.mean()` skips them without telling you. Tidy labels with `.str.strip().str.lower()`, and check `.value_counts()` before and after.
* **Put the fixes in one function.** Its first line should make a new table, so the table you pass in stays unchanged. Call it on at least two inputs to prove it's reusable.

```python
def clean_deliveries(df):
    df = df.drop_duplicates(subset="delivery_id")  # new table: original stays safe
    df["bags"] = pd.to_numeric(df["bags"], errors="coerce")
    df["country"] = df["country"].str.strip().str.lower()
    return df

clean_both = clean_deliveries(both)  # call it once...
clean_june = clean_deliveries(june)  # ...and again on a different input
```

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`.duplicated()` finds every repeat." | With no `subset=`, it only finds rows that match in *every* column. Match on the key. |
| "Coerce fixes a bad value like "TBD"." | It turns it into a new blank. Then you decide: drop, fill, or flag. |
| "Wrapping code in `def` makes it reusable." | It's reusable once you've called it on two or more different inputs. |

### How this connects

* **Next quest:** A clean table is where analysis starts. You'll group it and look for a pattern you can trust.
* **Boss Battle:** Part 2 asks for at least one cleaning function, called at least twice. Copy-pasting the same fix instead is one of the most common ways to lose points.

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

**Next:** [Quest 2.8 — Beneath the Total](quest-08-mining-a-pattern.md)
