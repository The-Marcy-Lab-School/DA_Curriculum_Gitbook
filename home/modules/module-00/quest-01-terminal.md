# Quest 0.1 — Meet Your Terminal: The Command Line (Day 1)

**Total time:** about 30 minutes

**Analyst toolkit:** **Use the terminal** · Understand data · Save with Git · Verify claims ([what's this?](introduction.md#the-big-picture-your-analyst-toolkit))

## Introduction

You already know how to find a file with a mouse. You open a folder, look inside, and double-click the next folder. Every one of those clicks has a typed version. For example, instead of double-clicking a folder called `photos`, you can type `cd photos` and press Return.

Typing feels slow at first. But it's exact, you can repeat it, and many data tools only work this way.

In this reading, you'll learn how to:

* find out which folder you're in, and list what's inside it
* move into a folder, and back out of it
* print a file on the screen
* read an error message when a command doesn't work

**Main takeaway:** In a new folder, check where you are and what's there before you do anything else. Then move, and check again.

**Why it matters at work:** Almost every data job starts in the terminal: you find the project folder, look at the files, and run your tools there. People notice when a new analyst checks where they are first, instead of guessing.

## Learning goals

After this reading, you should be able to say:

* I can use `pwd` and `ls` to find out where I am and what's in a folder.
* I can use `cd` with a relative path to move into a folder, and `cd ..` to move back up.
* I can read a `command not found` error and fix my typo.

**Skills:** Terminal & Command Line

## Quick recall

This is the first quest, so these come from everyday life and from the Module 0 Introduction.

* Recall that every file on your computer lives inside a folder, and folders can hold other folders. Your Documents folder is one example.
* Recall that the **terminal** is the window you type in, and the **shell** (zsh on a Mac) is the program inside it that runs your commands. You read about both in [the Module 0 Introduction](introduction.md#the-terminal-and-the-shell).

## New software: Terminal

**What it's for:** Terminal is **software** that comes with every Mac. It opens a window where you type commands to your computer instead of clicking. Inside the window runs a **shell**, a program that reads each command and runs it. On a Mac, the shell is called **zsh**. For more about the terminal and the shell, see [the Module 0 Introduction](introduction.md#the-terminal-and-the-shell).

To open Terminal, press **Command + Space**, type `Terminal`, and press **Return**.

**How you'll see it in this reading:**

```bash
pwd               # where am I?
ls                # what's here?
cd plants         # move into plants
cd ..             # move up one level
cat tomatoes.txt  # print a file
git --version     # is git installed?
```

<details>
<summary>Expand to walk through the code</summary>

1. `pwd` prints the folder you're in now, as a full path, like `/Users/sam/garden`. It changes nothing.
2. `ls` lists the files and folders inside the folder you're in. It changes nothing.
3. `cd plants` moves you into the `plants` folder. It prints nothing when it works. That silence is normal.
4. `cd ..` moves you up one level, back to the folder that holds the one you're in. Two dots always mean "up one level."
5. `cat tomatoes.txt` prints everything in the file `tomatoes.txt`, without opening any app.
6. `git --version` asks whether Git, a tool you'll meet later in this module, is installed. If it is, it prints a version number. If your Mac asks to install "command line developer tools," click **Install**.

</details>

In the reading, each command line starts with `$`. On your Mac, the line may end in `%` instead. Both are the **prompt**: the terminal's sign that it's ready. You never type it yourself.

**Learn more:** [Apple: Terminal User Guide](https://support.apple.com/guide/terminal/welcome/mac) (official) · [W3Schools: Bash tutorial](https://www.w3schools.com/bash/) (bash is another shell. The basic commands work the same way in zsh.)

## Words to know

### The window and what you type: Terminal basics

| Word | What it means |
| --- | --- |
| **Terminal** | A window where you type text commands to your computer instead of clicking. On a Mac, the software is called Terminal. |
| **Command line** | The line in the terminal where you type a command. People also use "the command line" to mean working in the terminal in general. |
| **Shell** | The program inside the terminal that reads your command and runs it. A Mac uses the zsh shell. |
| **Command** | One typed instruction, like `pwd` or `ls`. The terminal runs it when you press Return. |
| **Prompt** | The sign at the start of the line, like `$` or `%`, that says the terminal is ready for a command. You never type it. |
| **Output** | What the terminal prints back after a command runs. Some commands print nothing when they work. |
| **Error message** | Output that says a command didn't work. It names the exact word it didn't understand, like `zsh: command not found: pdw`. |

### Where am I?: Folders and paths

A **directory** is another word for a folder. Programmers say "directory," so you'll see both words.

| Word | What it means |
| --- | --- |
| **Directory** | A folder. It can hold files and other folders. `cd` stands for "change directory." |
| **Home folder** | Your own folder on the computer. It's named after you, like `sam`. The terminal often starts here. |
| **Working directory** | The folder the terminal treats as "here" right now. Most commands act on it. `pwd` prints it. |
| **Path** | The written location of a file or folder, with a `/` between each folder name. |
| **Absolute path** | The full route from the top of the computer, like `/Users/sam/garden/plants`. It starts with `/` and works from anywhere. |
| **Relative path** | A route that starts from the working directory. From inside `garden`, the path `plants` means "the plants folder right here." |
| **`..` (two dots)** | The folder that holds the one you are in: up one level. |

![Left: the garden folder drawn as a tree. The home folder sam holds garden, which is marked You are here. garden holds README.md, notes, and plants. plants holds peppers.txt and tomatoes.txt. An arrow labeled cd plants goes down from garden into plants, and an arrow labeled cd .. goes back up. Under the tree: the absolute path to plants is /Users/sam/garden/plants, and the relative path from garden is plants. Right: five commands. pwd answers Where am I? and prints /Users/sam/garden. ls answers What is here? and prints README.md notes plants. cd plants moves into plants and prints nothing. cd .. moves up one level and prints nothing. cat tomatoes.txt prints the file.](images/m0-garden-folders.svg)

## Before you read

In the reading, you'll focus on a community garden (a shared garden where neighbors grow plants together). Its laptop has a folder called `garden`, with plant lists and notes inside.

Think about: when you open a new folder with your mouse, what are the first two things you notice? What do you think the typed version of each one is? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. What `pwd` prints, and why running it can't hurt anything.
2. The difference between the paths `plants` and `/Users/sam/garden/plants`.
3. What the terminal prints when you mistype `pwd` as `pdw`, and which word the message names.

**[Start the reading: Meet Your Terminal →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod0/dev-environment/reading-1-meetterminal/)** (about 22 minutes)

## Main takeaways

### Summary

* **Look before you move.** In any new folder, run `pwd` (Where am I?) and `ls` (What's here?). Neither one changes anything.
* **`cd` moves you, not your files.** `cd plants` uses a relative path to go into a folder right here. `cd ..` goes up one level. An absolute path, like `/Users/sam/garden`, works from anywhere.
* **Read the error before you retry.** `command not found: pdw` names the exact word the shell didn't know. Fix the typo, not the computer.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "`cd notebooks` moves my files into a new place." | It moves *you*. Your working directory changes. The files stay where they are. |
| "`cd` printed nothing, so it didn't work." | Silence means it worked. Run `pwd` to check where you are now. |
| "An error message means I broke something." | It usually means a typo. The message names the word it didn't understand. |
| "I need to type the `$` too." | The `$` or `%` is the prompt. Type only the command after it. |
| "`ls` only shows a folder's contents the first time." | It shows the current contents every time you run it. |

### How this connects

* **Next reading:** You'll look inside a data file, like an animal shelter's list of pets, and decide what kind of value each column holds: text, a whole number, a decimal, true/false, or a date. An **animal shelter** is a place that cares for pets until a new family takes them home. The reading starts with two warm-up questions about `cat` and `ls`.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll use the terminal to find your project folder, look at the files inside it, and open a data file before you analyze it.

## Quick check

**1.** You're inside a folder called `data-project`. It holds `data`, `notebooks`, and `README.md`. You run `cd notebooks`. What changed?

* A. Your working directory: the folder you're in.
* B. Where your project files are saved.
* C. The name of the project.

<details>
<summary>Answer</summary>

**A.** `cd` changes your working directory. It doesn't move any files or rename anything.

</details>

**2.** You type `sl` and the terminal prints `zsh: command not found: sl`. What happened, and what do you do next?

<details>
<summary>Answer</summary>

It's a typo. The shell doesn't know the word `sl`, and the message names it. Type `ls` instead.

</details>

---

**Next:** [Quest 0.2 — What Kind of Data Is This? Data Types and Data Structures (Day 1)](quest-02-data-literacy.md)
