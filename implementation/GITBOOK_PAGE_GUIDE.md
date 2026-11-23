# GitBook Page Guide

How every module in this GitBook is built, starting with Module 2.
This folder sits outside `home/`, so GitBook does not publish it.
Module 2 (`home/modules/module-02/`) is the reference: when this guide and a Module 2 page disagree, fix whichever one is wrong.

## Goals

1. A first-time reader can follow every page without help.
2. Each page says what the reader is about to learn, and why it matters for a data job, before it teaches anything.
3. Every page has the same shape, so readers spend their energy on the ideas, not on finding things.
4. Readers can name the skills they're building and say them out loud in an interview.

## Writing rules

- **Plain words, about a 6th-grade reading level.** Short sentences, one idea each. Cut any word that adds nothing.
- **Define every term the first time it appears**, in the page's "Words to know" section. Include the terms a reader needs even when the interactive reading skips them (for example, *measures of central tendency* or *variance*).
- **Say what units a result comes in** whenever a page teaches a number: dollars, minutes, rows, a percent, or squared units.
- **Never name a tool, function, or term before it's defined.** This matters most in "How this connects": describe what the reader will *do* next, not the name of a tool they haven't met.
- **No emojis** in headings or body text.
- **Game words always come with a plain name.** Keep the quest titles, but every game word is paired with what it actually is, in parentheses: **Quest 2.1 — The Loudest Number (Descriptive Statistics)**, **Boss Battle (Module Project)**, **Checkpoint (Review and Solo Practice)**. Don't use other game words ("mission", "unlock", "arena", "reload", "conquer").
- **Say it once.** Don't repeat the same point in three places on one page.
- **GitBook hint blocks** (`{% hint style="info" %}`) are for the one or two lines a reader must not miss. At most two per page. Never use one for the page's opening; that's the Introduction's job.
- **Answers stay hidden** in `<details>` blocks, so readers try first.
- **No module numbers or day numbers in "Quick recall."** Describe what the reader did ("Recall that you built a function that…"), and link the earlier page by its title.

## Pictures

- Add a diagram when it explains something words can't: a process, a decision, a shape, or a comparison.
- Save diagrams as SVG in the module's `images/` folder, with a white background and the blue (`#1D4ED8`) and orange (`#C2410C`) palette, so they work for colorblind readers.
- **Text size:** body labels at least 17px and axis labels at least 20px in the SVG's own units. GitBook shrinks wide images to fit the page, so anything smaller becomes hard to read.
- **Every chart has a labeled x-axis and y-axis**, even a sketch.
- Every image needs alt text that says what it shows.
- Before merging, render each SVG and look at it: no text should touch or cross a box edge.

## Videos

Each interactive reading ends with an optional video. When a video explains something better than the reading does:

1. **Preferred:** turn the video's key picture into a diagram on the GitBook page (or in the reading), and keep the video as optional extra help.
2. **If the video is the clearest explanation of a core idea:** make it required, place it before the reader needs the idea, and say so in the page's Read section ("Watch this 6-minute video first").

Only mark a video required after someone has watched it and confirmed it's the clearest explanation.

## Page types and order in the sidebar

| Order | Page | File | Purpose |
|---|---|---|---|
| 1 | Module Introduction | `README.md` | Where you've been, where you're going, why it matters |
| 2 | Module Overview | `overview.md` | The route, new tools, skills, and how each page works |
| 3 | Quest | `quest-NN-<slug>.md` | One page per reading |
| 4 | Practice Day | `practice-day-<n>.md` | Review days with no new reading |
| 5 | Checkpoint (Review and Solo Practice) | `checkpoint.md` | Self-check before the Boss Battle |
| 6 | Module Conclusion | `conclusion.md` | What you can do now, how to say it, and where it shows up next |

**There is no Boss Battle page.** Project scenarios, deliverables, and lengths change from cohort to cohort, so the GitBook only describes the project at the skill level ("you'll describe key columns of a real dataset") and says the instructor shares the details. Never list project deliverables, file names, topics, or grading points in the GitBook.

**There are no separate tool pages.** A new tool is introduced in a "New tool" section on the quest page where it first appears (see the Quest template).

## Templates

### Module Introduction (`README.md`)

1. **Where you've been**: 3 to 5 bullets on earlier skills this module uses.
2. **Where you're going**: what this module teaches, in 2 or 3 sentences.
3. **Why it matters for data work**: one real example of what goes wrong without these skills.
4. **The big picture**: one diagram of the module's workflow.
5. **Next**: link to the Module Overview.

### Module Overview (`overview.md`)

1. **Your route**: a table of day, page (with its plain name), and a one-line goal. Include practice days, the Checkpoint, the Conclusion, and the Boss Battle (Module Project) days, without linking a project page.
2. **New tools**: one line each, with the quest where its "New tool" section lives.
3. **Skills you'll build**: a table of skill (rubric name), what it means in plain words, and where you'll practice it.
4. **What the words mean**: Quest, Practice Day, Checkpoint, Boss Battle, each with its plain name.
5. **How each quest page works**: the quest sections in order.

### Quest (`quest-NN-<slug>.md`)

1. **Title**: `Quest M.N — <Quest title> (<Plain topic name>)`, then one line: `**Day X** · Reading time: about N minutes`
2. **Introduction** (heading: `## Introduction`): 3 to 5 sentences.
   - Open with a short, everyday hook and a concrete example ("Sometimes averages can be misleading. For example, …").
   - Say what this reading covers.
   - End with the main takeaway, starting "The main takeaway: …"
   - Then one line: `**Why it matters at work:** …`
3. **Learning goals**: a checklist (`- [ ] I can …`), 3 items, with "Check off each goal once you can do it." Then a **Skills:** line with the rubric skill names.
4. **Quick recall**: 1 to 3 bullets reminding the reader of something they already did that this reading builds on. Start each with "Recall that…". Include a line of code when it helps. Link the earlier page by its title. No module or day numbers.
5. **New tool: <name>** (only when the reading introduces a tool or package). Three parts, nothing more:
   - **What it's for:** 1 or 2 sentences.
   - **How you'll see it in this reading:** the actual lines from the reading, in a code block with a short comment on each line.
   - **Learn more:** 2 or 3 links: the official docs, and W3Schools when it has a page.
6. **Words to know**: tables of *Word | What it means*. When there are more than 8 terms, split them into small groups with a one-line heading each (for example, "What is typical?" and "How spread out?"). Add a *Units* column when the terms are numbers.
7. **Before you read**: no hidden answer. Pick the version that fits:
   - **Scenario:** "In the reading, you'll focus on <scenario>. Think about: <question>. Write down your first answer, then see if the reading agrees."
   - **First answer:** "What's your first answer to <question>? Write it down, then check it against the reading."
   - **Spot the problem** (when the Introduction already covers the idea): "Here's an answer: '<plausible but wrong claim>'. Something is off about it. What? See if the reading agrees with you."
8. **Read**: first "As you read, look for:" with 3 numbered prompts, **then** the reading link and its time.
9. **Main takeaways**:
   - **Summary**: 3 bullets, bold lead-in on each.
   - **Common mix-ups**: table of *If you think… | What's actually true*.
   - **How this connects**: two bullets.
     - **Next reading:** what the reader will *do* next, in plain words, with no undefined tool or function names.
     - **Boss Battle (Module Project):** where this skill shows up, at the skill level only.
10. **Quick check**: 2 questions, answers hidden.
11. **Next**: one link.

### Practice Day and Checkpoint

1. **Title** with its plain name: `Practice Day (Review)` or `Module M Checkpoint (Review and Solo Practice)`.
2. **Introduction**: what the day is for, in 2 or 3 sentences.
3. **What happens in class.**
4. **Self-check questions**, answers hidden, each tagged with the quest to revisit.
5. **Checkpoint only:** an "I can" readiness checklist for the Boss Battle (Module Project).

### Module Conclusion (`conclusion.md`)

Comes after the Checkpoint and before the Boss Battle (Module Project).

1. **Introduction**: celebrate what the reader has done, with real numbers (readings, datasets, labs).
2. **What you can do now**: a table by workflow step.
3. **How to talk about your skills**: one resume line per skill group, with blanks for project details, and the interview answer frame.
4. **Where these skills show up next**: first in the Boss Battle (Module Project), then a table mapping this module's skill to its version in later modules.
5. **Before you move on**: 3 quick self-checks.
6. **Next**: the Boss Battle (Module Project), with "your instructor will share the project details", then the next module.

## Skills language

Use the curriculum's skill names exactly as the rubric does (for example, **Data Cleaning & Imputation**), so the GitBook, the readings, the tracker, and the rubric all match. Each skill appears in three places:

1. The Module Overview's skills table
2. The **Skills:** line on each quest
3. The conclusion's "How to talk about your skills" section

## Checklist before merging a module

- [ ] Every reading URL and "Learn more" link opens.
- [ ] Every relative link and image path resolves.
- [ ] `SUMMARY.md` lists every page in sidebar order, with plain names in parentheses.
- [ ] No emojis, and no game word without its plain name.
- [ ] No link to a Boss Battle page, and no project deliverables or topics named.
- [ ] No tool or function named before its "New tool" section or "Words to know" entry.
- [ ] Each quest's takeaways match what its reading actually teaches.
- [ ] Each diagram rendered and checked for text size and overlap.
