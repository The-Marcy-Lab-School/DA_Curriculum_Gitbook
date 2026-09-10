## Your Mission

A column can contain numbers without actually representing a quantity.

As a data analyst, one of your first jobs is to figure out **what the data represents before deciding what to do with it**.

**Target:** Distinguish Variables, Values, Data Types, and Data Structures—and classify data based on what it represents, not simply what it looks like.

---

## Vocabulary Mission

By the end of this quest, you should be able to recognize, use, and explain:

* **Variable**
* **Value**
* **Data Type**
* **String**
* **Integer**
* **Float**
* **Boolean**
* **Data Structure**

You don't need perfect definitions yet.

Your mission during the reading is to notice **what makes each term different**.

---

## 🎮 Prediction Challenge: Number or Not?

Imagine you receive a dataset containing this column:

| ZIP Code |
| -------- |
| `07030`  |
| `00501`  |
| `10001`  |

Every value contains digits.

### Lock In Your Prediction

Which claim would you defend?

**A.** ZIP Code is quantitative because it contains numbers.

**B.** ZIP Code may contain digits without representing a measurable quantity.

Choose **A or B** and write down one reason for your choice.

**Don't look anything up yet.**

You'll return to this prediction after the Main Mission.

---

# 🎯 Main Mission — REQUIRED

This interactive reading is the **required learning mission for this quest**.

Your Prediction Challenge prepared you for it. Now your job is to work through the full reading and build the knowledge you'll need for the checkpoint.

## What to Hunt For

As you work, pay attention to the relationship between:

**Variable → Value → Data Type → Data Structure**

Watch especially for:

* Situations where something **looks numeric but isn't meant for arithmetic**.
* Clues that help distinguish **Structured Data from Unstructured Data**.

## 🚀 Launch the Required Reading

[**Start: Name It, Tag It, Group It →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/dev-environment/reading-2-whatkindofdata/)

**Required:** Complete the interactive reading before continuing to the checkpoint.

When you finish, return here and test what you can retrieve **without reopening the reading**.

---

# ⚡ Checkpoint: Vocabulary Lightning Round

**No reading. No notes. Retrieval only.**

For each term below, see whether you can explain what it means in **one clear sentence**:

* **Variable**
* **Value**
* **Data Type**
* **String**
* **Integer**
* **Float**
* **Boolean**
* **Data Structure**

### Score Your Retrieval

Give yourself:

* **Ready** — I can explain it clearly without help.
* **Almost** — I recognize it, but my explanation needs work.
* **Reload** — I need to revisit this term.

Any **Almost** or **Reload** term becomes part of your next review round.

The goal isn't a perfect score.

The goal is knowing **what your brain can retrieve without help**.

---

## 🎮 Classification Challenge

For each value, decide which Data Type is the best match.

| Value        | Your Classification |
| ------------ | ------------------- |
| `"Brooklyn"` | ?                   |
| `27`         | ?                   |
| `19.95`      | ?                   |
| `True`       | ?                   |
| `"00501"`    | ?                   |

**Make your classifications before opening the Hint or Answer.**

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Think about what each value **represents** and how it would be used.

Ask yourself:

* Is it text?
* Is it a whole number used for arithmetic?
* Does it contain a decimal?
* Does it represent a true/false state?
* Could treating digits as a number change the meaning of the value?

</details>

Try the classifications one more time before revealing the Answer.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

One reasonable classification is:

| Value        | Classification |
| ------------ | -------------- |
| `"Brooklyn"` | String         |
| `27`         | Integer        |
| `19.95`      | Float          |
| `True`       | Boolean        |
| `"00501"`    | String         |

The important idea is that **appearance alone doesn't determine how data should be treated**.

For example, `"00501"` contains digits, but treating it as an Integer could remove the leading zeros and change the identifier.

</details>

### Defend Your Choice

Choose **one** classification and explain what evidence led you to that decision.

---

## 🧩 Structure Check

Without reopening the reading:

**What's one clue you could use to decide whether data is Structured or Unstructured?**

Try to explain your reasoning in one or two sentences.

If you're unsure, add **Structured vs. Unstructured** to your Reload list before the Module 0 Checkpoint.

---

## 🧠 Boss Question: The ZIP Code Trap

Return to your original prediction.

A teammate says:

> “ZIP Codes are made of numbers, so we should store them as quantitative values.”

### Your Challenge

Identify what's wrong with that reasoning.

Your explanation should address:

* **What a ZIP Code represents.**
* **Whether arithmetic on ZIP Codes would be meaningful.**
* **What could happen to a value like `00501` if it were treated as an Integer.**

Write your explanation before opening the Hint.

<details>
<summary>💡 Hint — Open After Your First Attempt</summary>

Don't focus only on what the characters **look like**.

Ask yourself:

**What does the value mean, and what operations would actually make sense for it?**

Also consider what could happen to the leading zeros in `00501`.

</details>

Now improve your original response.

Only open the Answer after making your second attempt.

<details>
<summary>✅ Answer — Open After Your Second Attempt</summary>

A ZIP Code functions as an **identifier**, not a measured quantity.

Arithmetic such as adding or averaging ZIP Codes would not produce a meaningful result.

Storing `00501` as an Integer can also remove its leading zeros, changing the identifier from `00501` to `501`.

The key lesson:

**Digits do not automatically make a variable quantitative.**

</details>

---

# 💼 Interview Arena

**One Question. One Strong Answer.**

An interviewer asks:

> **“What's the difference between a Data Type and a Data Structure?”**

Think through your answer before revealing help.

<details>
<summary>💡 Hint — Open If You're Stuck</summary>

Think at two different levels:

**Data Type:** What kind of value is this?

**Data Structure:** How are values organized together?

</details>

<details>
<summary>✅ Example Answer — Open After You've Answered</summary>

A Data Type describes the kind of value you're working with and helps determine what operations make sense for that value.

A Data Structure describes how values are organized so they can be stored and worked with together.

So, **Data Type is about the kind of value, while Data Structure is about how values are organized.**

</details>

---

## 🏁 Final Check

You're ready for the next quest when you can:

* Distinguish a **Variable** from its **Value**.
* Identify common **Data Types**.
* Distinguish a **Data Type** from a **Data Structure**.
* Identify a clue that distinguishes **Structured from Unstructured Data**.
* Explain why digits do not automatically make something quantitative.
* Defend an appropriate type choice for an identifier such as a ZIP Code.
* Answer the Interview Arena question clearly using technical vocabulary.

If one of these still feels shaky, that's useful information.

**Reload that skill before unlocking the next quest.**

---

## 🔓 Next Unlock

Next, you'll move from identifying data to navigating the environment where you'll work with it.

[**Continue to Quest 0.2 — Meet Your Terminal →**](quest-02-terminal.md)
