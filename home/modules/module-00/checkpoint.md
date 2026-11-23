# Module 0 Checkpoint: Review and Practice (Day 7)

**Time:** about 10 minutes (no new reading)

**Analyst toolkit:** **Use the terminal** · **Understand data** · **Save with Git** · **Verify claims** (all four) ([what's this?](introduction.md#the-big-picture-your-analyst-toolkit))

## Introduction

You've finished all four quests. This page checks what you can do on your own, without the readings or your notes. Answer each question first, then open the answer. Each question names the quest to review if you miss it.

**Main takeaway:** The questions you miss show you which quest to review before the Boss Battle (Module Project).

**Why it matters at work:** On a new job, nobody tells you which skills you still need to practice. Analysts who can check their own understanding learn faster and make fewer mistakes.

**Skills:** Data Literacy · General Programming & Coding · Critical Thinking · Terminal & Command Line · Git & Version Control · AI Literacy

## Self-check questions

Try each one before you open the answer. If you miss one, go back to the quest in parentheses.

**1. (Quest 0.1)** You're in a project folder. You want to see what's there, then move into a folder called `data`. Which two commands do you run?

<details>
<summary>Answer</summary>

```bash
ls       # see what's here
cd data  # move into data
```

`ls` looks. `cd` moves. Run `pwd` after, if you want to check where you are.

</details>

**2. (Quest 0.1)** `pwd` prints `/Users/sam/data-project/notebooks`. Which command takes you back to `data-project`?

<details>
<summary>Answer</summary>

`cd ..`. Two dots mean "up one level," and `data-project` is the folder that holds `notebooks`.

</details>

**3. (Quest 0.2)** A file has a column called `student_id`, with values `00182`, `00491`, and `01327`. A teammate says, "They're all numbers, so we should store them as numbers." What's wrong with that?

<details>
<summary>Answer</summary>

A student ID is a label, not an amount. Nobody adds or averages IDs. Stored as a whole number, `00182` loses its first zeros and becomes `182`, which could match the wrong student. Store it as text. Digits alone don't make something a number.

</details>

**4. (Quest 0.2)** Name the data type of each value: `"Brooklyn"`, `27`, `19.95`, `True`, `"00501"`.

<details>
<summary>Answer</summary>

| Value | Data type |
| --- | --- |
| `"Brooklyn"` | Text (string) |
| `27` | Whole number (integer) |
| `19.95` | Decimal (float) |
| `True` | True/false (Boolean) |
| `"00501"` | Text (string). It's a ZIP code: a label, and its first zeros matter. |

</details>

**5. (Quest 0.2)** A shop has two files. One is a CSV of orders, with the same columns on every row. The other holds customer reviews, written as paragraphs. Which one is structured data, and how can you tell?

<details>
<summary>Answer</summary>

The orders file is structured: every row has the same columns. The reviews are unstructured: free text with no rows or columns.

</details>

**6. (Quest 0.3)** You change your project and make a commit. You open GitHub, but the change isn't there. What's missing?

<details>
<summary>Answer</summary>

A push. A commit is saved only on your laptop. `git push` sends it to GitHub.

</details>

**7. (Quest 0.3)** A classmate plans to edit a project all week and make one commit on Friday, "so the history looks clean." What's the problem?

<details>
<summary>Answer</summary>

One big commit mixes every change together. If something breaks midweek, there's no earlier checkpoint, and no way to tell which edit caused it. Small commits with clear messages, made as you go, are easier to use later.

</details>

**8. (Quest 0.4)** An AI tool says, "This dataset has exactly 8,250 rows." You have the file. Name one real way to check the claim.

<details>
<summary>Answer</summary>

Open the file and count the rows yourself. Any check works if it uses a real source. Asking the AI "are you sure?" doesn't count, because it's the same source making the same claim.

</details>

**9. (Quest 0.4)** A job candidate says, "If ChatGPT gives me a detailed explanation and the code runs, I know the answer is right." What's wrong with that?

<details>
<summary>Answer</summary>

A detailed answer can still be a hallucination, and code that runs only proves there was no error. The result can still be wrong. Check it against something real: the original data, a small example where you know the answer, or a trusted source.

</details>

**10. (All four quests)** You get a dataset you've never seen. Which way of working sounds more like an analyst?

* A. Open the file, trust your first impression, ask an AI tool, and turn it in.
* B. Look at the data, decide what each column means, check every claim, and save your work in small commits.

<details>
<summary>Answer</summary>

**B.** It uses all four skills: you understand the data, work in the right folder, check claims instead of trusting them, and keep a history of how your work grew. That makes your work easy to check and to trust.

</details>

## Explain the picture

Look at each picture. Explain it out loud in two or three sentences, as if to a classmate. Then open the answer.

**1. (Quest 0.2)**

![Three panels. Variable: the box pet_of_the_week holds "Biscuit" in week 1 and "Mango" in week 2. Data type: "Biscuit" is text, 3 is a whole number, 12.5 is a decimal, True is true/false, and 2026-09-14 is a date. Data structure: one pet's record holds Mango's name, age, weight, adopted, and arrived values, and the whole pets.csv file holds one record for every pet.](images/m0-name-tag-group.svg)

<details>
<summary>Answer</summary>

A variable is a labeled box. The name `pet_of_the_week` stays the same, but its value changes from `"Biscuit"` to `"Mango"`. A data type says what kind of value something is, like text or a decimal. A data structure groups many values together: one pet's record, or the whole file of pets.

</details>

**2. (Quest 0.3)**

![A flow from left to right: your folder, then git add, then the staging area, then git commit, then commits saved on your laptop, then git push, then GitHub. Steps 1 to 3 are Git, software on your laptop. Step 4 is GitHub, a website. A commit is not on GitHub until you push it.](images/m0-add-commit-push.svg)

<details>
<summary>Answer</summary>

You edit a file in your folder. `git add` stages the change, and `git commit` saves it as a snapshot on your laptop. All of that is Git, and it needs no internet. `git push` sends your commits to GitHub, a website where others can see them. Until you push, a commit is only on your laptop.

</details>

## Interview practice

Answer each question out loud in two or three sentences. Then open the example answer.

> **"What's the difference between `cd` and `ls`?"**

<details>
<summary>Example answer</summary>

`cd` changes the folder I'm working in. `ls` lists what's inside a folder. I use `ls` to look around, and `cd` to move.

</details>

> **"What's the difference between a data type and a data structure?"**

<details>
<summary>Example answer</summary>

A data type is the kind of one value, like text, a whole number, or true/false. It tells you what you can do with it. A data structure is how many values are grouped together, like one record or a whole table. So a data type is about one value, and a data structure is about how values are organized.

</details>

> **"What's the difference between committing and pushing in Git?"**

<details>
<summary>Example answer</summary>

A commit saves a snapshot of my changes in the repository on my laptop. A push sends my commits to a remote, like GitHub, so others can see them. Committing saves my history. Pushing shares it.

</details>

> **"How do you check an answer you get from an AI tool?"**

<details>
<summary>Example answer</summary>

I treat it as an unverified claim. I find the exact claim, like a number or a source. Then I check it against something real, like the original data or the source it names. I only use it once the evidence agrees, and I fix or drop it if it doesn't.

</details>

## Ready for the Boss Battle (Module Project)?

You're ready when you can say "I can" to each of these:

* I can use `pwd`, `ls`, `cd`, and `cat` to find my way around a project folder and look at a file.
* I can decide what kind of data a column holds by what it means, not only by what it looks like.
* I can explain why an ID made of digits should be stored as text.
* I can tell structured data from unstructured data.
* I can stage, commit, and push my work, with a clear message for each commit.
* I can explain the difference between a commit and a push, and between Git and GitHub.
* I can check an AI claim against a real source before I use it.

---

**Next:** [Module 0 Conclusion (Day 8)](conclusion.md)
