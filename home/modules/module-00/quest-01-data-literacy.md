# Quest 0.1 — What Kind of Data Is This?

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

**Don't look anything up yet.** You'll return to this prediction after the Main Mission.

---

# 🎯 Main Mission — REQUIRED

This interactive reading is the **required learning mission for this quest**.

Your prediction challenge prepared you for it. Now your job is to work through the full reading and build the knowledge you'll need for the checkpoint.

## What to Hunt For

As you work, pay attention to the relationship between:

**Variable → Value → Data Type → Data Structure**

Watch especially for situations where something **looks numeric but isn't meant for arithmetic**.

## 🚀 Launch the Required Reading

[**Start: Name It, Tag It, Group It →**](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/dev-environment/reading-2-whatkindofdata/)

**Required:** Complete the interactive reading before continuing to the checkpoint.

When you finish, return here and test what you can retrieve **without reopening the reading**.

---

# ⚡ Checkpoint: Vocabulary Lightning Round

**No reading. No notes. Retrieval only.**

For each term below, see whether you can explain what it means in **one clear sentence**:

* Variable
* Value
* Data Type
* String
* Integer
* Float
* Boolean
* Data Structure

### Score Your Retrieval

Give yourself:

* **Ready** — I can explain it clearly without help.
* **Almost** — I recognize it, but my explanation needs work.
* **Reload** — I need to revisit this term.

Any **Almost** or **Reload** term becomes part of your next review round.

The goal isn't a perfect score. The goal is knowing **what your brain can retrieve without help**.

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

Now choose **one** of your answers and explain what evidence led you to that classification.

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
* **What could happen to a value like `00501` if it were treated as an integer.**

### Need Another Attempt?

If your first explanation only says *“ZIP Codes should be strings,”* try again.

**Hint:** Don't focus only on what the characters look like. Ask what the value **means** and what operations make sense for it.

### Check After Your Second Attempt

**Answer:** A ZIP Code functions as an identifier rather than a measured quantity. Arithmetic such as averaging ZIP Codes would not produce a meaningful result, and storing `00501` as an integer can remove its leading zeros and change the identifier.

---

# 🎙️ Interview Arena: Record → Replay → Improve

Imagine an interviewer asks:

> **“What's the difference between a Data Type and a Data Structure?”**

### Round 1 — Record

Use your phone, laptop, or another available recording tool.

Record a **30–60 second answer** without reopening the reading.

### Round 2 — Replay

Listen to your answer once.

Check whether you:

* Defined **Data Type** clearly.
* Defined **Data Structure** clearly.
* Explained the difference between them.
* Used technical vocabulary accurately.
* Gave an example only if it made your explanation clearer.

### Round 3 — Improve

Write down **one thing you would improve**.

Then record your answer one more time.

Your second answer should be **clearer, not necessarily longer**.

---

## 🏁 Final Check

You're ready for the next quest when you can:

* Distinguish a **Variable** from its **Value**.
* Identify common **Data Types**.
* Distinguish a **Data Type** from a **Data Structure**.
* Explain why digits do not automatically make something quantitative.
* Defend an appropriate type choice for an identifier such as a ZIP Code.
* Explain one of these distinctions clearly in an interview-style response.

---

## 🔓 Next Unlock

Next, you'll move from identifying data to navigating the environment where you'll work with it.

[**Continue to Quest 0.2 — Meet Your Terminal →**](quest-02-terminal.md)

