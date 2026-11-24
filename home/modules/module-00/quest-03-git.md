# Quest 0.3 — Save the Story of Your Work: Git and Version Control (Days 2–3)

**Total time:** about 60 minutes

**Analyst toolkit:** Use the terminal · Understand data · **Save with Git** · Verify claims ([what's this?](introduction.md#the-big-picture-your-analyst-toolkit))

## Introduction

Have you ever saved a file as `essay_final.docx`, then `essay_final_v2.docx`, then `essay_REAL_final.docx`? After a week, nobody knows which copy is right, or what changed between them.

There's a better way. You keep one file, and you save a series of checkpoints. Each checkpoint has a short note that says what changed.

In these two readings, you'll learn how to:

* turn a project folder into a repository that saves its history
* save a snapshot of your work, with a message that says what changed
* send your saved work to GitHub, a website where others can see it
* save small changes often, instead of one big change at the end

**Main takeaway:** Saving a snapshot on your laptop (a commit) and sharing it online (a push) are two separate steps. Commit small, clear changes as you go.

**Why it matters at work:** Teams use Git to share and review work. A clear history shows what changed, when, and why. If something breaks, you can find the exact change that caused it.

## Learning goals

After this reading, you should be able to say:

* I can stage a change (pick it for my next commit) with `git add` and save it with `git commit`, with a message that says what changed.
* I can explain the difference between a commit and a push, and between Git and GitHub.
* I can explain why several small commits make a more useful history than one big commit.

**Skills:** Git & Version Control · Terminal & Command Line

## Quick recall

* Recall that `cd` moves you into a folder and `ls` lists what's inside it, from [Meet Your Terminal](quest-01-terminal.md). Every Git command is typed inside a project folder, so you'll start each time with `cd`.
* Recall that you ran `git --version` in [Meet Your Terminal](quest-01-terminal.md) to check that Git is installed. Now you'll use it.

## New software: Git

**What it's for:** Git is **software** on your own laptop. It saves the history of a project folder as a series of snapshots, each with a message about what changed. It doesn't need the internet. Git is the most common tool for **version control**: keeping track of every version of your work.

**How you'll see it in this reading:**

```bash
git init                 # start a repository
git status               # what's going on?
git add notes.md         # stage one file
git commit -m "Add first tree counts"
git log --oneline        # list saved commits
git diff                 # show changed lines
```

<details>
<summary>Expand to walk through the code</summary>

1. `git init` turns the folder you're in into a **repository**: a folder whose history Git tracks. Git keeps that history in a hidden folder called `.git`. No snapshots are saved yet.
2. `git status` tells you what's going on: which files changed, and which are ready to save. It never changes anything, so you can run it any time.
3. `git add notes.md` puts the changes in `notes.md` into the **staging area**: the list of changes you've picked for your next snapshot. Files you edited but didn't add stay out.
4. `git commit -m "Add first tree counts"` saves everything in the staging area as one **commit**, a snapshot. `-m` stands for "message." The text in quotes after it is the commit message.
5. `git log --oneline` lists every saved commit, newest first. Each line shows the commit's short ID (short for identifier: a code that labels that one commit), then its message.
6. `git diff` shows the exact lines you changed that aren't committed yet. A line starting with `-` was removed. A line starting with `+` was added.

</details>

**Learn more:** [Pro Git: About Version Control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) (official, from Git's own team) · [W3Schools: Git tutorial](https://www.w3schools.com/git/)

## New website: GitHub

**What it's for:** GitHub is a **website**, not software you install. It holds a copy of your repository online, so other people can see it and work on it too. Git saves your history on your laptop. GitHub shares a copy of it. You'll need a free GitHub account.

**How you'll see it in this reading:**

```bash
git remote add origin https://github.com/you/tree-notes.git
git push -u origin main
git push
```

<details>
<summary>Expand to walk through the code</summary>

1. `git remote add origin <url>` tells Git where your online copy lives, and gives it the short name `origin`. The URL is the repository's address on GitHub.
2. `git push -u origin main` sends your commits to `origin`. `main` is the name Git gives your project's history by default (when you don't choose a different name). `-u` tells Git to remember where to push.
3. After that first time, plain `git push` is enough.

</details>

**Learn more:** [GitHub Docs: About GitHub and Git](https://docs.github.com/en/get-started/start-your-journey/about-github-and-git) (official) · [W3Schools: Get started with GitHub](https://www.w3schools.com/git/git_remote_getstarted.asp)

## Words to know

### Saving your history: Version control

| Word | What it means |
| --- | --- |
| **Version control** | Keeping track of every version of your work, so you can see what changed, when, and go back if you need to. |
| **Repository (repo)** | A project folder whose history Git tracks. `git init` starts one. |
| **Commit** | A saved snapshot of your project at one moment, with a message about what changed. Later edits become new commits. They don't change old ones. |
| **Commit message** | The short note saved with a commit. A good one starts with an action word and names the change, like `Fix count on block 2`. |
| **Staging area** | The list of changes you've picked for the next commit. `git add` puts a change there. |
| **Untracked** | A file Git can see but isn't saving yet. `git add` it to start saving it. |
| **Working tree clean** | What `git status` prints when every change is already committed. Nothing is waiting. |

### Sharing your work: Remotes

| Word | What it means |
| --- | --- |
| **Remote** | A copy of your repository kept somewhere else, like on GitHub. |
| **`origin`** | The usual short name for your main remote. |
| **Push** | Sending the commits on your laptop up to a remote, so they show up there too. Until you push, a commit is only on your laptop. |
| **Clone** | Making your own copy of a repository that's already on a remote, with its whole history. |

![A flow from left to right. 1, Your folder: you edit notes.md. git add moves the change to 2, the staging area, which holds the changes picked for the next commit. git commit saves them as 3, commits: snapshots saved on your laptop. git push sends them to 4, GitHub, a copy online that other people can see. A bracket over steps 1 to 3 says Git: software on your laptop, no internet needed. A bracket over step 4 says GitHub: a website. A note underneath says a commit is not on GitHub until you push it.](images/m0-add-commit-push.svg)

### How often to save: Commit habits

| Word | What it means |
| --- | --- |
| **Atomic commit** | A commit that holds exactly one focused change, like "fix the test date." *Atomic* here means "one small piece that stands alone." |
| **Commit granularity** | How much one commit covers, from one small edit to a whole day of mixed work. Smaller is usually easier to read later. |
| **Commit cadence** | How often you commit as you work. A good habit: commit each time you finish one change you can describe in a short sentence. |

![Two outputs of git log --oneline for the same afternoon of work. Left, one big commit: 51fe55a updates, then e01019b Start the study guide. Three changes are mixed into one commit called updates. Right, three small commits, newest first: 2be44a6 Fix a typo in the README, d48a131 Add a section on fractions, b6c0073 Fix the test date, and 2121428 Start the study guide. Each change has its own commit and message.](images/m0-one-vs-three-commits.svg)

## Before you read

In the first reading, you'll focus on three neighbors who count the trees on their street. They keep the counts in one shared notes file. Over three weeks, one fixes a wrong count, one adds a new column, and one rewrites a confusing sentence.

Think about: a month later, how could one neighbor find out who changed the count on block 2, and when? Write down your first answer, then see if the reading agrees.

## Read

This quest has two readings. Do them in this order.

### Part 1: Git Saves the Story

As you read, look for:

1. Why `git init` says the new repository is "empty."
2. What `git status` says about `notes.md` after `git add`, but before `git commit`.
3. Where a commit is saved before anyone runs `git push`.

**[Start the reading: Git Saves the Story →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/git-github/reading-1-gitsavesthestory/)** (about 22 minutes)

### Part 2: Build the Git Habit

As you read, look for:

1. Why one commit called "updates" makes the fractions mistake hard to find a week later.
2. What the `-` and `+` signs mean in the output of `git diff`.
3. What `git status` prints once every change is committed.

**[Start the reading: Build the Git Habit →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/git-github/reading-2-buildthegithabit/)** (about 22 minutes)

## Main takeaways

### Summary

* **Git saves snapshots on your laptop.** `git add` stages a change, and `git commit -m "..."` saves the staged changes as one commit with a message. Run `git status` any time to see what's going on.
* **A commit is not a push.** Commits stay on your laptop until `git push` sends them to a remote like GitHub. Git is the software that saves. GitHub is the website that shares.
* **Commit small and often, with clear messages.** One focused change per commit. Check `git diff` first, then write a message that names the change, like `Fix the test date`.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I committed, so it's on GitHub." | A commit is saved only on your laptop. You still need to `git push`. |
| "Editing a file gets it ready to commit." | You must stage it with `git add` first. |
| "`git init` saves my first snapshot." | It only starts the repository. You still add and commit. |
| "Git and GitHub are the same thing." | Git is software on your laptop. GitHub is a website that holds a copy. |
| "One big commit on Friday keeps the history clean." | It mixes every change together and leaves no earlier checkpoint if something breaks midweek. |
| "`git status` might change my files." | It only reports. It never changes anything. |

### How this connects

* **Next reading:** An AI (artificial intelligence) chatbot will give you an answer that sounds very sure, with a number and a source. A chatbot is a program that answers questions in everyday language. You'll check it against the real data file, step by step, before you decide whether to trust it.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll save your project as you go, in small commits with clear messages, and push them to GitHub. Your history will show how your work grew, step by step.

## Quick check

**1.** Which commit message tells a reader the most about what changed?

* A. `stuff`
* B. `update`
* C. `Add notes on column data types`

<details>
<summary>Answer</summary>

**C.** It starts with an action word and names the change. Someone reading the history a month from now can tell what happened without opening any file.

</details>

**2.** You edit `notes.md`, then run `git commit -m "Fix count on block 2"`. Git doesn't make a commit. Its message says `no changes added to commit`. What did you forget?

<details>
<summary>Answer</summary>

You forgot to stage the change. Run `git add notes.md` first, then commit again.

</details>

---

**Next:** [Quest 0.4 — Confidence Is Not Evidence: Checking AI Answers (Day 6)](quest-04-ai-verification.md)
