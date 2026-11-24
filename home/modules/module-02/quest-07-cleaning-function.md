# Quest 2.7 — Write It Once: Cleaning Functions (Day 8)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → **Clean** → Explore → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Some data problems happen again and again. For example, every Monday a gym gets a sign-up sheet for its classes. This week's sheet has 6 rows, but only 5 people signed up:

* Ana is listed twice.
* "Yoga" is spelled three ways: "Yoga", "yoga", and "YOGA".

If you count the rows for each class, Yoga looks like three different classes. And it shows 4 Yoga sign-ups for only 3 people. Fixing this by hand every week is slow, and one day you'll forget a step. In the picture below, look at the red rows on the messy sheet.

![Two sign-up sheets side by side. Left, the messy sheet has 6 rows. Ana signs up for Yoga twice, and the repeated row is red. Yoga is spelled three ways, Yoga, yoga, and YOGA, and the two odd spellings are red. Counting each class gives Yoga 2, yoga 1, YOGA 1, and Spin 2, so Yoga looks like 3 classes, with 4 sign-ups for 3 people. Right, the clean sheet has 5 rows, one per person, and every label is lowercase. Counting gives yoga 3 and spin 2: one yoga class with 3 people.](images/gym-signups-repeats-spellings.svg)

**Main takeaway:** Write your cleaning steps once, in a **reusable function**. A reusable function is one you call on two or more different tables. In the reading, that's the May list and the June list. Calling it on a second table is how you prove it works on every new file.

**Why it matters at work:** A cleaning function fixes the same problems in every new file, the same way each time. For example, analysts use one to:

* clean a sales report that arrives every Monday
* stack the customer lists from two stores, then remove the customers who are on both
* tidy the spelling of product names before they count sales for each product

If you fix each file by hand, you'll skip a step one week. Then that week's counts will be wrong.

## Learning goals

After this reading, you should be able to say:

* I can stack two tables and remove repeated records (rows about the same real thing) using a key column.
* I can turn text into numbers and tidy up labels, then count what changed.
* I can write a cleaning function and prove it's reusable by calling it on two different inputs.

**Skills:** Data Cleaning & Imputation · Functions & Modular Programming (from Module 1)

## Quick recall

* In [Look Before You Filter](quest-02-inspect-filter.md), you found repeated rows with `df.duplicated()` and number columns stored as text (`str`). Then, in [Drop, Fill, or Flag](quest-06-missing-data.md), you chose to drop, fill, or flag each gap.
* `.strip()` removes spaces from both ends of a string, and `.lower()` makes every letter lowercase, so `" Peru ".strip().lower()` gives `"peru"`. In this reading, they run on a whole column.
* Your validation function in Module 1's [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md) checked each record against rules, and [One Job at a Time](../module-01/quest-07-second-function.md) gave each function one job. A cleaning function uses both ideas.

## Words to know

The examples use the reading's two delivery lists from Terra Bean, a coffee shop. The May list has 5 rows and the June list has 5 rows.

### Problems in a file

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Stack** | Put one table under another, so their rows end up in one table. | May's 5 rows + June's 5 rows = **10 rows** |
| **Duplicate row** | The same real-world record showing up more than once, often after stacking two lists that overlap. | Delivery D104 is in both May and June. |
| **Key column** | A column whose value names one record. | `delivery_id`, like `D104` |
| **Number stored as text** | A column of numbers that pandas loaded as text (`str`), because at least one value isn't a number. Math on it gives errors or wrong answers. | June's `bags` column, because one value is `"TBD"` (short for "to be determined") |
| **Label** | A value in a category column, like a country name. | `"Kenya"`, `"kenya "`, and `" Kenya"` are three different labels to pandas. |

### Stacking and repeats

| Code | What it does | Example in the reading |
| --- | --- | --- |
| **`pd.concat([may, june], ignore_index=True)`** | Stacks the two tables, top to bottom. Setting the parameter `ignore_index` to `True` numbers the rows from 0 again, so no row label shows up twice. | Rows numbered 0 to 9 |
| **`.duplicated(subset="delivery_id")`** | Marks a row True when it repeats an earlier row. Setting the parameter `subset` to `"delivery_id"` means: compare only the `delivery_id` column, even if other columns differ. | Finds **2** repeats: D104 and D105 |
| **`.drop_duplicates(subset="delivery_id")`** | Removes the repeats, and keeps the first copy of each ID. | 10 rows − 2 repeats = **8 rows** |

### Text into numbers

| Code | What it does | Example in the reading |
| --- | --- | --- |
| **`pd.to_numeric(...)`** | Turns a column of text into numbers. On its own, it stops with a `ValueError` at the first value that isn't a number. | Stops at `"TBD"` in June's `bags` |
| **Coerce** | Force a change. Setting the parameter `errors` to `"coerce"` means a value that can't become a number becomes NaN ("not a number," pandas' mark for a blank) instead of stopping with an error. | `"TBD"` becomes NaN, so June's `bags` has **1 blank** |

### Tidying labels

You know `.strip()` and `.lower()` on one string. **`.str`** lets you use them on a whole column at once:

* One string: `"PERU".lower()` gives `"peru"`.
* A whole column: `both["country"].str.lower()` makes every country lowercase. Without `.str`, `both["country"].lower()` gives an error, because a column isn't a string.

| Code | What it does | Example in the reading |
| --- | --- | --- |
| **`.str`** | Lets a column use the string methods you already know. `.str.lower()` runs `.lower()` on every value in the column. | `both["country"].str.lower()` |
| **`.strip()`** | Removes spaces from the start and end of text. | `" Kenya"` becomes `"Kenya"`. |
| **`.lower()`** | Makes every letter lowercase. | `"PERU"` becomes `"peru"`. |
| **`.value_counts()`** | Counts how many rows hold each different value in a column. Good for spotting one label spelled more than one way. | Before: Kenya in 3 spellings (2 + 1 + 1 rows). After: **kenya 4** |

### Functions

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Helper function** | A small one-job function that another function calls. | `tidy_text` inside `clean_deliveries` |
| **Reusable function** | A function called two or more times on different inputs. A one-time script wrapped in `def` and called once isn't reusable yet. | `clean_deliveries` runs on the stacked table and on June alone. |
| **`assert`** | Stops the notebook with an error if its condition is False. A quick self-test. | `assert clean_both["delivery_id"].duplicated().sum() == 0` |

## Before you read

In the reading, you'll focus on Terra Bean, a small coffee shop that gets a list of bean deliveries every month. The May list and the June list have 5 rows each. June repeats two May deliveries, spells Kenya three ways, and says "TBD" where one bag count should be.

Think about: after you stack the two lists into one table, how many rows will it have, and how many real deliveries? Write down your first answer, then see if the reading agrees.

## ⭐ Read

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

The picture below shows the cleaning function's three steps, in order.

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
| "`.duplicated().sum()` gave 0, so there are no repeats." | With no `subset=`, it only finds rows that match in *every* column. On the stacked table, it finds 0. Matching on `delivery_id` finds 2: D104 and D105. D105 came back with a corrected count, 10 bags instead of 9. |
| "`errors="coerce"` fixed the 'TBD' value." | It turned "TBD" into a blank (NaN), so June's `bags` now has 1 blank. You still decide: drop, fill, or flag. |
| "`.str.lower()` makes all the Kenya labels match." | Spaces still split them: "kenya " and " kenya" stay different. Strip first, then lowercase. Then all 4 Kenya rows say "kenya". |
| "I put my code in a `def`, so it's reusable now." | It's reusable once you've called it on two or more different inputs. `clean_deliveries` runs on the stacked table and gives 8 rows, then on June alone and gives 5. |

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
