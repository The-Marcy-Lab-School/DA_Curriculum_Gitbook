# Quest 2.9 — The Pattern Isn't the Proof (Day 10)

{% hint style="info" %}
**In one sentence:** A pattern can be real in the file and still be wrong about the world, so ask specific questions about where the data came from before you trust it.
{% endhint %}

## Why this matters

Data is collected by people, with choices and gaps built in. If a neighborhood looks like it has few trees only because volunteers walked fewer of its blocks, new trees get planted in the wrong place. Good analysts ask the questions that catch this, and they ask them in a way someone can actually answer.

## What you'll be able to do

* I can read a dataset's source note and find the questions it leaves open.
* I can check data for Origin, Completeness, and Bias, and count rows and blanks by group in code.
* I can turn a vague question into a checkable one that a data steward could answer.

**Skills:** Critical Thinking

## Words to know

| Word | What it means |
| --- | --- |
| **Source note** | The short document that comes with a dataset: who collected it, when, and how. Read it first. |
| **Origin** | Who collected this, and how? |
| **Completeness** | What's missing, and why? |
| **Bias** | Who or what got counted less than the rest? |
| **Data steward** | The person or team who looks after the data and can answer questions about it. |
| **Checkable question** | A question specific enough that a data steward could answer it with a fact. |
| **Generic question** | A question that could fit any dataset, like "Is this data accurate?" Nobody can answer it. |

## Before you read

A tree count shows West has only 2 trees, the fewest of four areas. Does West have the fewest trees?

<details>
<summary>Answer</summary>

Maybe. It could also mean volunteers walked only a few blocks in West. The file alone can't tell you which. The reading shows how to find out.

</details>

## Read

**[Start the reading: The Pattern Isn't the Proof →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/interrogating-your-data/reading-1-the-pattern-isnt-the-proof/)** (about 19 minutes)

As you read, look for:

1. What the source note answers, and what it leaves open.
2. Why a total of 4 blanks hides something that a count by group shows.
3. How to rewrite "Why is data missing?" into a question someone can answer.

## Main takeaways

### Summary

* **Read the source note first.** It answers some questions and shows which ones are still open.
* **Check every dataset for Origin, Completeness, and Bias.** Count rows and blanks *by group* in code before you quote a number: `df["col"].isna().groupby(df["group"]).sum()`.
* **Ask checkable questions.** A good one names a group, a number, or a method, and ties to something you found.

| Checklist | The question it asks | Example from the tree count |
| --- | --- | --- |
| **Origin** | Who collected this, and how? | A school club counted South on one rainy morning. |
| **Completeness** | What's missing, and why? | 3 of South's 4 trees have no species. |
| **Bias** | Who or what got counted less? | West has 2 rows. The other areas have 3 or 4. |

| Generic (nobody can answer) | Checkable (a steward can answer) |
| --- | --- |
| "Is this data accurate?" | "Which blocks did West's volunteers walk, and how many?" |
| "Why is data missing?" | "3 of South's 4 trees have no species. Did the club leave species blank when they weren't sure?" |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "If the file shows it, it's true." | A file shows what was collected. How it was collected can create the pattern. |
| "'Is this data accurate?' is a careful question." | It sounds careful, but there's no fact that answers it. |
| "The total number of blanks tells me enough." | Blanks bunched in one group can throw off every comparison between groups. |

### How this connects

* **Next quest:** The same habit applies to AI. When an AI describes a chart, you check each claim against the real numbers.
* **Boss Battle:** Your memo needs 2 checkable questions about your data. Before you code, you'll also write Question, Assumption, and Risk notes about what your stakeholder didn't tell you.

## Quick check

**1.** A fall tree count uses a phone app for South and volunteers on foot everywhere else. The app finds twice as many trees in South. Which question goes to the data steward?

* A. "Is the app data reliable?"
* B. "Did the app count trees on the same blocks the volunteers walked, or on more blocks?"
* C. "Are there more trees in South now?"

<details>
<summary>Answer</summary>

**B.** It's specific and checkable. A is generic, and C is the question the data can't answer until B is settled.

</details>

**2.** Name the three rows of the checklist.

<details>
<summary>Answer</summary>

Origin (who collected it, and how), Completeness (what's missing, and why), and Bias (who or what got counted less).

</details>

---

**Next:** [Quest 2.10 — Two Sets of Eyes](quest-10-ai-on-charts.md)
