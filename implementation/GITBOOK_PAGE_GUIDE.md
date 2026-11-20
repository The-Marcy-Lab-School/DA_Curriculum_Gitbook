# GitBook Page Guide

How every module in this GitBook is built, starting with Module 2.
This folder sits outside `home/`, so GitBook does not publish it.

## Goals

1. A first-time reader can follow every page without help.
2. Each page says why the topic matters for a data job before it teaches anything.
3. Every page has the same shape, so readers spend their energy on the ideas, not on finding things.
4. Readers can name the skills they're building and say them out loud in an interview.

## Writing rules

- **Plain words, about a 6th-grade reading level.** Short sentences, one idea each. Cut any word that adds nothing.
- **Define every term the first time it appears**, in the page's "Words to know" table.
- **No emojis in headings or body text.** Keep the quest titles; drop the game words around them ("mission", "unlock", "arena"). The one exception is "Boss Battle", which stays as the nickname for the project.
- **Say it once.** Don't repeat the same point in three places on one page.
- **Use GitBook hint blocks** (`{% hint style="info" %}`) for the one or two lines a reader must not miss. At most two per page.
- **Add a picture when it explains something words can't**: a process, a decision, a shape, or a comparison. Put SVG diagrams in the module's `images/` folder. Each one needs alt text that says what it shows.
- **Answers stay hidden** in `<details>` blocks, so readers try first.

## Page types and order in the sidebar

| Order | Page | Purpose |
|---|---|---|
| 1 | Module Introduction (`README.md`) | Where you've been, where you're going, why it matters, skills and tools |
| 2 | Tool Guide (`tool-<name>.md`) | One short page per new tool, placed in the sidebar just before the first quest that uses it |
| 3 | Quest (`quest-NN-<slug>.md`) | One page per reading day |
| 4 | Practice Day (`practice-day-<n>.md`) | Recall days with no new reading |
| 5 | Checkpoint (`checkpoint.md`) | Self-check before the project |
| 6 | Project / Boss Battle (`project.md`) | What to build, day by day, and how it's graded |
| 7 | Module Wrap-Up (`wrap-up.md`) | What you can do now, how to say it, and where it shows up next |

## Templates

### Module Introduction

1. **Where you've been**: 3 to 5 bullets on earlier modules' skills that this module uses.
2. **Where you're going**: what this module teaches, in 2 or 3 sentences.
3. **Why it matters for data work**: what a working analyst does with these skills.
4. **The big picture**: one diagram of the module's workflow.
5. **Your route**: a table of quests, days and one-line goals, including practice days.
6. **New tools**: one line each, linking to the tool guides.
7. **Skills you'll be expected to show**: a table of skill, plain meaning, where you'll practice it, and how the project checks it.
8. **The Boss Battle**: 3 sentences on the project.
9. **How to use each quest page**: the page's sections in order, so readers know what to expect.

### Tool Guide (about one screen)

1. **In one sentence**: what the tool is.
2. **Why analysts use it**: 2 or 3 sentences.
3. **What you'll learn about it in this module**: table of quest to skill.
4. **The few lines you'll use most**: a small code block.
5. **Common first-day problems**: 2 or 3, each with its fix.
6. **Getting started resources**: 3 or 4 links, official docs first.

### Quest

1. **Title**: `Quest M.N — <Reading title> (Day X)`
2. **In one sentence**: hint block
3. **Why this matters**: 2 or 3 sentences tied to a real data job
4. **What you'll be able to do**: 3 "I can" statements
5. **Skills** and **new tool today** (if any)
6. **Words to know**: table, 5 to 8 terms
7. **Before you read**: one warm-up question, answer hidden
8. **Read**: link, time, and 3 "look for" prompts
9. **Main takeaways**: Summary (3 bullets), Common mix-ups (table), How this connects (next quest + project part)
10. **Quick check**: 2 questions, answers hidden
11. **Next**: one link

### Module Wrap-Up

1. What you did (numbers: readings, datasets, skills)
2. What you can do now: a checklist of "I can" statements
3. How to say it: one resume line and one interview answer per skill group
4. Where these skills show up next: table of this module's skill to next module's version of it
5. Before you move on: 3 quick self-checks
6. Link to the next module

## Skills language

Use the curriculum's skill names exactly as the rubric does (for example, **Data Cleaning & Imputation**), so the GitBook, the readings, the tracker and the rubric all match. Each skill appears in four places:

1. The module intro's skills table (what it means, where you'll practice it)
2. The "Skills" line on each quest
3. The project rubric section
4. The wrap-up's "How to say it" section

## Checklist before merging a module

- [ ] Every reading URL opens.
- [ ] Every relative link and image path resolves.
- [ ] `SUMMARY.md` lists every page in sidebar order.
- [ ] No emojis left in headings or body text.
- [ ] Each quest's takeaways match what its reading actually teaches.
