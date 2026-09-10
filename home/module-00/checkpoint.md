# ⚡ Module 0 Checkpoint

## Ready for the Final Mission?

You've completed all four Module 0 quests.

Before you take on the Boss Battle, prove that you can retrieve and connect the skills you've been building.

**No readings. No notes on your first attempt.**

Let's see what's ready.

---

## 🎮 Challenge 1 — The Identifier Trap

You receive a dataset with this column:

| Student ID |
| ---------- |
| `00182`    |
| `00491`    |
| `01327`    |

A teammate says:

> “They're all numbers, so Student ID should be treated as a quantitative variable.”

What's wrong with that reasoning?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Ask yourself:

**What does this value represent?**

Would calculating the average of these IDs tell you anything useful?

What could happen to the leading zeros?

</details>

Try again before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

Student ID is an **identifier**, not a measured quantity.

Even though it contains digits, arithmetic on Student IDs would not be meaningful. Treating a value such as `00182` as an Integer could also remove its leading zeros.

**Digits do not automatically make a variable quantitative.**

</details>

---

## 🎮 Challenge 2 — Terminal Navigation

You're inside a project directory.

You need to:

**1. See what's available.**
**2. Move into a directory named `data`.**

Which two commands could accomplish those jobs?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think:

**Inspect → Navigate**

One command lists what's available.

The other changes your current directory.

</details>

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

First, inspect:

```bash
ls
```

Then navigate:

```bash
cd data
```

`ls` helps you **inspect** a directory.

`cd` helps you **navigate** to another directory.

</details>

---

## 🎮 Challenge 3 — Commit ≠ Push

You make changes to your project and create a Commit.

You check GitHub, but the new changes aren't there.

**What might still need to happen?**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

A Commit records project history locally.

What action sends committed changes to a remote repository?

</details>

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

You may still need to **Push** your committed changes.

A **Commit** records a snapshot in your local Git repository.

A **Push** sends committed changes to a remote repository such as GitHub.

**Commit ≠ Push**

</details>

---

## 🎮 Challenge 4 — Confidence Is Not Evidence

An AI assistant tells you:

> “This dataset contains exactly 8,250 rows.”

You have access to the dataset.

What's **one concrete action** you could take to verify the claim?

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Don't ask only:

**“Are you sure?”**

Think about independent evidence you can inspect yourself.

</details>

Try again.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

You could inspect the dataset directly and determine its number of rows.

The important part isn't one specific tool or command.

It's that you verify the AI-generated claim using **independent evidence**.

**Claim → Check → Evidence → Trust**

</details>

---

# 🧠 Final Challenge — Connect the Skills

Imagine you're handed a public dataset you've never seen before.

Which workflow sounds more like the analyst you're becoming?

**A.**

**Open Dataset → Trust First Impression → Ask AI → Submit**

**B.**

**Inspect Data → Classify Carefully → Work Deliberately → Verify Claims → Preserve Your Work**

Choose your answer and explain **why**.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think across all four quests.

Your answer should connect more than one skill.

</details>

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

**B.**

Strong analysis starts before the final analysis itself.

You need to understand what the data represents, navigate your working environment, verify claims rather than accepting them automatically, and preserve meaningful project history with Git.

Those habits make your work easier to inspect, explain, and trust.

</details>

---

# 🏁 Readiness Check

You're ready for the Boss Battle when you can:

* Classify identifier-like data based on what it **represents**, not just how it looks.
* Use `ls` and `cd` to **Inspect and Navigate**.
* Explain why **Commit ≠ Push**.
* Name a concrete way to **verify an AI-generated claim**.
* Explain why these habits make analytical work more trustworthy.

### Something Still Shaky?

That's what this Checkpoint is for.

Go back to the relevant quest, reload the skill, and return when you're ready.

---

# 🔓 Boss Battle Unlocked

You've practiced the skills separately.

Now you'll use them together on data you haven't seen before.

[**Start the Module 0 Boss Battle — Data Literacy Field Notes →**](project.md)
