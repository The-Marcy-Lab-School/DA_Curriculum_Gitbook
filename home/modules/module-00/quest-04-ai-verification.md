# Quest 0.4 — Confidence Is Not Evidence: Checking AI Answers (Day 6)

**Total time:** About 30 minutes

**Analyst toolkit:** Use the terminal · Understand data · Save with Git · **Verify claims** ([what's this?](introduction.md#the-big-picture-your-analyst-toolkit))

## Introduction

Sounding sure and being right are two different things. For example, a friend tells you the store closes at 9 p.m. They sound completely sure. You get there at 8:30, and the doors are locked. It closed at 8.

AI (artificial intelligence) chatbots work the same way. A chatbot is a program that answers questions in everyday language. Chatbots give every answer in the same sure, polished tone, whether it's right or wrong.

**Main takeaway:** An answer's **confidence** tells you nothing about its **accuracy**. Confidence is how sure an answer sounds. Accuracy is whether it is correct. Only checking the answer against a real source tells you if it's accurate.

**Why it matters at work:** Analysts check AI answers before they share them with anyone. For example, they check:

* a row count or a total that an AI tool gives for a dataset (a set of data, often one table or file)
* a report or a website that an AI tool names as its source
* the result of code an AI tool wrote, against the real data

If you share a wrong number from an AI tool, you are responsible for it, not the tool.

## Learning goals

After this reading, you should be able to say:

* I can explain the difference between an unverified claim and a verified fact.
* I can check an AI claim against a real source: find the claim, find a source, compare, and decide.
* I can explain what a hallucination is, and why asking the same chatbot "are you sure?" is not checking.

**Skills:** AI Literacy · Critical Thinking

## Quick recall

* In [Meet Your Terminal](quest-01-terminal.md), `cat tomatoes.txt` printed everything in a file. In this reading, you'll use `cat` to open the real data file and check a number.
* [What Kind of Data Is This?](quest-02-data-literacy.md) split data into two groups: **structured** (rows and columns) and **unstructured** (free text). The reading opens by asking you to sort a chatbot's reply and a data file into these two groups.

## Words to know

### Is it true yet?: Claims and facts

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Claim** | A statement that something is true. | "Your volunteers collected 64 bags." |
| **Unverified claim** | A claim that nobody has checked yet. It might be right or wrong. Every AI answer starts here. | "64 bags," before anyone opens the cleanup log |
| **Verified fact** | A claim that someone has confirmed against a real, checkable source. | A bag total you added up yourself from the log |
| **Source** | Where information comes from, like the original data file, an official website, or a report you can open. | `cleanup_log.csv` |
| **Evidence** | What you find in a source that shows whether a claim is right or wrong. | The numbers in the log's `bags` column |
| **Verify** | To check whether something is true, using a source. *Verification* is the act of checking. | Add up the `bags` column, then compare the total with 64 |
| **Independent check** | A check that uses a different source from the one that made the claim. Asking the same chatbot again is not independent. | Opening `cleanup_log.csv` yourself |

### Why sure isn't the same as right: Confidence and accuracy

| Word | What it means | Example |
| --- | --- | --- |
| **AI chatbot** | A program that answers questions in everyday language. It writes by predicting which words usually come next. | ChatGPT or Claude |
| **Confidence** | How sure an answer *sounds*. | "64 bags, the most of any park cleanup this year," with no doubt in it |
| **Accuracy** | Whether an answer is actually *correct*. | Whether the log really adds up to 64 bags |
| **Hallucination** | A sure-sounding AI answer that is wrong. It may include a made-up number or a source that doesn't exist. | A news report, named with a year, that no one can find |

{% hint style="info" %}
**Asking "Are you sure?" is not checking.** The chatbot just makes a new claim, from the same place as the first one. To check, open a real source yourself.
{% endhint %}

## Before you read

In the reading, you'll focus on a park cleanup (a day when people pick up trash in a park). Volunteers wrote down every bag of trash they filled. Afterward, a chatbot says: "Your volunteers collected 64 bags of trash, the most of any park cleanup this year, according to a 2025 city news report."

Think about: before you print that sentence on a flyer (a printed page that shares news with many people), what would you check, and where? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. Why the chatbot's tone can't tell you whether its answer is right.
2. What the bags in the cleanup log (the written record of each volunteer's bags) add up to, compared with the chatbot's number.
3. What happens when the volunteer searches for the "2025 city news report."

**[Start the reading: Confidence Is Not Evidence →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/ai-literacy/reading1-confidenceisnotevidence/)** (about 20 minutes)

## Main takeaways

### Summary

* **Every AI answer is an unverified claim** until you check it against a real source, like the original data file.
* **Confidence is not accuracy.** A chatbot sounds just as sure when it's wrong. A specific number or a named source doesn't make an answer true.
* **Check in four steps:**
  1. Find the exact claim.
  2. Find a real source.
  3. Compare the two.
  4. Decide whether to use the claim, fix it, or drop it.

The picture below runs these four steps on the chatbot's answer about the park cleanup. Follow the steps from top to bottom.

![The chatbot's answer at the top: Your volunteers collected 64 bags of trash, the most of any park cleanup this year, according to a 2025 city news report. Below, four steps in order. 1, Find the claim: the number, 64 bags, and the source, a 2025 city news report. 2, Find a source: the cleanup log, cleanup_log.csv, and the city's news site. 3, Compare: 9 plus 12 plus 7 plus 10 plus 8 equals 46 bags, not 64, and there is no such report on the news site. 4, Decide: fix the number to 46 bags, and drop the report because it was made up. At the bottom: how sure an answer sounds does not tell you if it is true. Checking does.](images/m0-check-a-claim.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "It gave an exact number, so it's probably right." | A hallucination can be very exact. The chatbot said 64 bags. The log adds up to 9 + 12 + 7 + 10 + 8 = 46 bags. |
| "It named a source, so it's backed up." | The source may not exist. The volunteer searched the city's news site, and the 2025 report wasn't there. Search for it yourself. |
| "I asked the chatbot to double-check, and it agreed." | That's the same source making the same claim again. It's not an independent check. |
| "If AI-written code runs, the answer is right." | Running only means there was no error. Code that adds up the wrong column still runs and prints a total. Check the result against the real data. |
| "So I should never use AI." | Use it, but know which parts you've checked. In the reading, "46 bags" was safe to share only after someone added up the log. |

### How this connects

* **Next page:** In the Checkpoint, you'll answer questions from all four quests on your own, and find out which ones to review.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Before you write down a claim about your dataset (the set of data you'll work with), including one from an AI tool, you'll check it against the data itself and say how you checked.

## Quick check

**1.** An AI tool tells you, "There are 12,418 rows in this dataset." You have the data file open. What's the best next move?

* A. Use the number, because it's precise.
* B. Ask the AI whether it's sure.
* C. Check the file yourself.

<details>
<summary>Answer</summary>

**C.** You have the real source, so count the rows yourself. Asking the AI again only gives you another claim from the same place.

</details>

**2.** The chatbot also says, "Dev cleaned the playground." The log has the line `Dev,basketball court,12`. What do you do before you write a thank-you note?

<details>
<summary>Answer</summary>

Fix the claim. The log says Dev cleaned the basketball court, and Rosa cleaned the playground. The chatbot's sentence was a hallucination, so the note should follow the log.

</details>

---

**Next:** [Module 0 Checkpoint: Review and Practice (Day 7)](checkpoint.md)
