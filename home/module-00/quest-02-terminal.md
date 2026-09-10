# Quest 0.2 — Meet Your Terminal

### Your Mission

The Terminal gives you a direct way to communicate with your computer.

Instead of clicking through folders, you'll begin using commands to **inspect where you are and navigate where you need to go**.

**Target:** Use basic Terminal commands to navigate your environment and explain what those commands accomplish.

***

### Vocabulary Mission

By the end of this quest, you should be able to recognize, use, and explain:

* **Terminal**
* **Command Line**
* **Directory**
* **Path**
* **Command**
* `cd`
* `ls`

Keep this workflow in mind:

**Inspect → Navigate → Verify**

***

### 🎮 Warm-Up: Where Do You Go?

Imagine you're working with this project:

```
data-project/
├── data/
├── notebooks/
└── README.md
```

You're inside `data-project`, but you aren't sure what's available there.

What would be a useful first move?

**A.** Inspect the current directory.

**B.** Start changing directories without checking.

Lock in your answer and one reason why.

Don't look anything up yet.

***

## 🎯 Main Mission — REQUIRED

This interactive reading is the **required learning mission for this quest**.

Your goal isn't to memorize a giant list of commands.

Your goal is to understand how you can **navigate and communicate with your computer through the Terminal**.

### What to Hunt For

As you work through the reading, pay attention to:

* What `cd` accomplishes.
* What `ls` accomplishes.
* What a **Directory** represents.
* How commands help you navigate your computer.

Watch especially for the difference between:

**Navigating somewhere → Inspecting what's there**

### 🚀 Launch the Required Reading

[**Start: Meet Your Terminal →**](https://github.com/The-Marcy-Lab-School/DA_Curriculum_Gitbook/tree/mod0-gitbook-pilot/home/modules/module-00/REPLACE-WITH-VERIFIED-READING-URL/README.md)

**Required:** Complete the interactive reading before continuing.

When you finish, return here and test what you can retrieve **without reopening the reading**.

***

## ⚡ Checkpoint: Terminal Navigator

You're working inside:

```
data-project/
```

The project contains:

```
data-project/
├── data/
├── notebooks/
└── README.md
```

### Round 1 — Inspect

You want to see what's available in your current directory.

**What command would you run?**

<details>

<summary>💡 Hint — Open After Your First Attempt</summary>

You don't want to move anywhere yet.

You want to **list what's here**.

</details>

Try again before revealing the Answer.

<details>

<summary>✅ Answer — Open After Your Second Attempt</summary>

```bash
ls
```

`ls` lists the contents of a directory.

In this example, you would expect to see entries such as `data`, `notebooks`, and `README.md`.

</details>

***

### Round 2 — Navigate

You see the `notebooks` directory and decide that's where you need to work.

**What command would you run?**

<details>

<summary>💡 Hint — Open After Your First Attempt</summary>

This time you need to **change your current directory**.

</details>

Try again.

<details>

<summary>✅ Answer — Open After Your Second Attempt</summary>

```bash
cd notebooks
```

`cd` means **change directory**.

This command changes your current working directory to `notebooks`.

</details>

***

### Round 3 — Predict

You run:

```bash
cd notebooks
```

What actually changed?

**A.** Your current location in the file system.

**B.** The location of all your project files.

**C.** The name of the project.

<details>

<summary>💡 Hint — Open After Your First Attempt</summary>

Think about what **change directory** means.

Are you changing the project—or changing **where you're currently working inside it**?

</details>

<details>

<summary>✅ Answer — Open After Your Second Attempt</summary>

**A. Your current location in the file system.**

`cd notebooks` changes your current working directory.

It does not move your project files or rename the project.

</details>

***

### 🧭 Workflow Unlocked

When you're navigating an unfamiliar project, use:

#### Inspect → Navigate → Verify

**Inspect:** What's available where I am?

**Navigate:** Where do I need to go?

**Verify:** Did my command do what I expected?

You don't need to memorize every Terminal command.

You need to understand **what you're asking the computer to do**.

***

## 💼 Interview Arena

**One Question. One Strong Answer.**

An interviewer asks:

> **“What's the difference between `cd` and `ls`?”**

Think through your answer before revealing help.

<details>

<summary>💡 Hint — Open If You're Stuck</summary>

Think about two jobs:

**Navigate** versus **Inspect**.

Which command does each?

</details>

<details>

<summary>✅ Example Answer — Open After You've Answered</summary>

`cd` changes the directory I'm currently working in, while `ls` lists the contents of a directory.

So, I use `cd` to **navigate** through the file system and `ls` to **inspect** what's available at my current location.

</details>

***

### 🏁 Final Check

You're ready for the next quest when you can:

* Explain what the **Terminal** is used for.
* Recognize a **Directory** as a location in a file system.
* Explain what `cd` accomplishes.
* Explain what `ls` accomplishes.
* Choose between **Navigating** and **Inspecting** based on your goal.
* Use the **Inspect → Navigate → Verify** workflow.

If one of these still feels shaky, **reload that skill before moving forward**.

***

### 🔓 Next Unlock

You can now begin navigating your working environment from the Terminal.

Next, you'll learn how to preserve the story of your work using Version Control.

[**Continue to Quest 0.3 — Save the Story of Your Work →**](quest-03-git.md)
