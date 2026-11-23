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
- **Write for readers whose first language isn't English.**
  - Keep most sentences under 20 words. Split a sentence that lists three or more ideas into a short bulleted list.
  - Use the simple word instead of the hard word plus a gloss. Write "how much a claim usually pays," not "a typical (usual) claim."
  - When a hard word *is* the idea being taught (like *typical*, *spread*, *tendency*), explain it in plain words the first time: "**Typical** means usual or normal."
  - No idioms or slang ("gets old fast," "front and center," "on the job," "rep," "stands on its own").
  - Introduce an example with "For example, …", not "Here's an example."
- **Explain the "why" behind code facts**, not just the fact: "`sorted_gifts[1]` is the second item, *because Python starts counting positions at 0*."
- **Define every term the first time it appears**, in the page's "Words to know" section. Include the terms a reader needs even when the interactive reading skips them (for example, *measures of central tendency* or *variance*).
- **Say what units a result comes in** whenever a page teaches a number: dollars, minutes, rows, a percent, or squared units.
- **Never name a tool, function, or term before it's defined.** This matters most in "How this connects": describe what the reader will *do* next, not the name of a tool they haven't met.
- **No emojis** in headings or body text.
- **Game words always come with a plain name.** Keep the quest titles, but every game word is paired with what it actually is. In titles, put the plain name after a colon, so each title has only one set of parentheses (the day): **Quest 2.1 — The Loudest Number: Descriptive Statistics (Day 1)**, **Module 2 Checkpoint: Review and Solo Practice (Days 13–14)**. When a quest title ends in a question mark, skip the colon: **Quest 2.4 — Who's This Chart For? Exploratory vs. Explanatory Charts (Day 4)**. In body text, write **Boss Battle (Module Project)**. Don't use other game words ("mission", "unlock", "arena", "reload", "conquer").
- **Say it once.** Don't repeat the same point in three places on one page.
- **GitBook hint blocks** (`{% hint style="info" %}`) are for the one or two lines a reader must not miss. At most two per page. Never use one for the page's opening; that's the Introduction's job.
- **Answers stay hidden** in `<details>` blocks, so readers try first.
- **No module numbers or day numbers in "Quick recall."** Describe what the reader did ("Recall that you built a function that…"), and link the earlier page by its title.

## Technical terms

Use these words the same way on every page. Students learned *function*, *parameter*, *argument*, *module*, *class*, *object*, *method*, and *attribute* in Module 1, so use those exact meanings and say "recall that…" when it helps.

| Term | Use it for | Example |
| --- | --- | --- |
| **Tool** | The umbrella word for anything analysts use: a package, software, or a language. Never use it to mean a specific kind. | "four new tools" |
| **Software** | A program you open and use. | VS Code, Excel, Tableau, a web browser |
| **Package** (also *library*) | A collection of Python code other people wrote. You install it once with `pip`, then load it with `import`. Say "package" first; mention "library" once as another name. | NumPy, pandas, Matplotlib |
| **Module** | One file of Python code you `import`. Some come with Python; a package is made of many. | `json`, `os`, `matplotlib.pyplot` |
| **File type** | Something you open and run in software, not something you import. | a Jupyter notebook (`.ipynb`), a CSV |
| **Function** | Named code you call with parentheses. | `np.mean(gifts)`, `pd.read_csv(...)`, `plt.title(...)` |
| **Class / object** | A class describes one kind of thing; an object is one thing made from it. | `DataFrame` is a class; `df` is a DataFrame object |
| **Method** | A function that belongs to an object. Has parentheses. | `df.sort_values(...)`, `.round(2)` |
| **Attribute** | A value stored on an object. No parentheses. | `df.shape`, `df.dtypes` |
| **Parameter / argument** | A parameter is the name a function expects; the argument is the value you pass in. Write "the parameter `ddof` is set to `1`", never "the parameter `ddof=1`". | `ddof`, `ascending`, `subset` |
| **Series** (pandas) vs. **data series** (charts) | A pandas Series is one column of a table. A data series is one set of values drawn on a chart. Never let the two share a name on a page. | `df["site"]` vs. one line on a line chart |

## Code blocks

- **Keep comments short.** A comment should never wrap to a second line: about 30 characters at most (`import numpy as np  # load the package`). Many lines need no comment at all.
- **Explain the code in a "Code walkthrough" under the block**, as a numbered list with one item per line or idea. This keeps the code readable and the explanation complete.
- **Introduce every parameter by name, then its argument.** "This line sets the parameter `ddof` to the argument `1`. That tells NumPy to use the sample formula…" Never open with a bare `ddof=1`, and never call `ddof=1` itself "the parameter." Recall *parameter* and *argument* the first time a module uses them.
- Keep code lines under about 65 characters so they don't scroll sideways.

## Pictures

- **Every quest page gets at least one picture.** Pick the kind that fits the idea:

  | Kind | Use it when the idea is… | Module 2 examples |
  | --- | --- | --- |
  | **Flow** | steps in order | `four-checks.svg`, `cleaning-pipeline.svg`, `ai-claim-check.svg` |
  | **Decision tree** | a choice that depends on answers | `drop-fill-flag.svg`, `chart-chooser.svg` |
  | **Concept map** | how things relate to each other | `tools-map.svg`, `three-questions.svg`, `two-pages.svg` |
  | **Side-by-side comparison** | the same data shown two ways, or before and after | `skew-shapes.svg`, `axis-baseline.svg`, `confound-gap.svg` |
  | **Worked example** | what code does to a table | `groupby-split-apply-combine.svg` |

- **Use the reading's own numbers and names** in the picture, and check them against the reading.
- **Don't repeat a table in a picture.** If a picture shows the same thing as a table, keep one.
- **Revisit the most important pictures.** The module's workflow diagram appears in the Introduction and again in the Conclusion. The Checkpoint has an "Explain the picture" section where readers explain two key diagrams from memory.
- Save diagrams as SVG in the module's `images/` folder, with a white background and the blue (`#1D4ED8`) and orange (`#C2410C`) palette, so they work for colorblind readers.
- **Text size:** body labels at least 17px and axis labels at least 20px in the SVG's own units. GitBook shrinks wide images to fit the page, so anything smaller becomes hard to read.
- **Every chart has a labeled x-axis and y-axis**, even a sketch.
- **Show shapes, don't just name them.** When a page names shapes or patterns (left-skewed, symmetric, right-skewed), show them side by side in one picture.
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
| 0 | Module header | `README.md` | Only the module's name and one line pointing to the Overview. It exists so the module shows as one item in the sidebar that readers expand. |
| 1 | Overview of Module M (Read FIRST) | `overview.md` | What the module is about, the route, new tools, where each skill is practiced, game words, and how each page works |
| 2 | Module Introduction | `introduction.md` | Where you've been, where you're going, why it matters |
| 3 | Quest | `quest-NN-<slug>.md` | One page per reading |
| 4 | Practice Day | `practice-day-<n>.md` | Review days with no new reading |
| 5 | Checkpoint: Review and Solo Practice | `checkpoint.md` | Self-check before the Boss Battle |
| 6 | Module Conclusion | `conclusion.md` | What you can do now, how to say it, and where it shows up next |

**There is no Boss Battle page.** Project scenarios, deliverables, and lengths change from cohort to cohort, so the GitBook only describes the project at the skill level ("you'll describe key columns of a real dataset") and says the instructor shares the details. Never list project deliverables, file names, topics, or grading points in the GitBook.

**There are no separate tool pages.** A new tool is introduced in a "New tool" section on the quest page where it first appears (see the Quest template).

## Templates

### Module header (`README.md`)

GitBook needs a page for every item that expands in the sidebar, so keep this page almost empty: `# Module M: <Module name>`, then "Start with the [Overview of Module M (Read FIRST)](overview.md). Then follow the pages in the sidebar, in order." In `SUMMARY.md`, list it as `Module M: <Module name>`, with the Overview as its first child.

### Overview of Module M (Read FIRST) (`overview.md`)

1. **Title**: `Overview of Module M: <Module name> (Read FIRST)`, then **Time**.
2. **What this module is about**: 2 or 3 sentences.
3. **What the words mean**: Quest, Practice Day, Checkpoint, Boss Battle, each with its plain name.
4. **Your route**: a table of day, page (with its plain name), and a one-line goal. Include practice days, the Checkpoint, the Conclusion, and the Boss Battle (Module Project) days, without linking a project page.
5. **New tools**: one line each, linking to the quest's "New tool" section.
6. **Where you'll practice each skill**: a table of skill (rubric name) and the quests that practice it. The meanings live on the Introduction page.
7. **How each quest page works**: the quest sections in order.
8. **Next**: the Module Introduction.

### Module Introduction (`introduction.md`)

1. **Where you've been**: 2 to 5 bullets on earlier skills this module uses. No module numbers.
2. **Where you're going**: what this module teaches, in 2 or 3 short sentences.
3. **Why it matters for data work**: one real example of what goes wrong without these skills ("For example, a manager at…").
4. **The big picture: the <name> workflow**: define *workflow*, show the diagram, then a table of each step and the question it answers. End with the tracker line exactly as quest pages show it.
5. **What you'll be able to do**: the module's outcomes, one bullet per workflow step.
6. **Skills you'll build**: every rubric skill, grouped (for example: Working with numbers, Preparing data, Showing and telling, Thinking critically), with a plain meaning for each.
7. **The Boss Battle (Module Project)**: its own section, written to excite. Say what students will do as the analyst, that they'll run the whole workflow on their own, and what they'll have at the end. Stay at the skill level: no topics, deliverables, or file names. End with "Your instructor will share the dataset choices and the exact requirements."
8. **Next**: the first quest.

### Quest (`quest-NN-<slug>.md`)

1. **Title**: `Quest M.N — <Quest title>: <Plain topic name> (Day X)`, the same in `SUMMARY.md` and in every "Next" link, so readers always know which day they're on (Module 1 uses the same `(Day X)` ending). Practice days, the Checkpoint, and the Conclusion end with their day too. Then one line at the very top with the **total** time, counting both the GitBook page and the interactive reading: `**Day X** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)`. Estimate the page at 150 words a minute (a careful pace for beginners and English learners), rounded to 5 minutes. Every other page type gets a **Time** line too.
2. **Workflow tracker**, right under the time line: `**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#…))`, with the quest's step in bold. Practice days and checkpoints bold every step they review. The Conclusion shows the workflow diagram again.
3. **Introduction** (heading: `## Introduction`), in this order:
   - A short, everyday hook and a concrete example, in short sentences ("Sometimes averages can be misleading. For example, …"). Use a different example from the reading's own scenario.
   - "In this reading, you'll learn how to:" followed by 2 to 4 short bullets.
   - `**Main takeaway:**` in one or two short sentences.
   - `**Why it matters at work:**` in one or two short sentences.
4. **Learning goals**: a checklist (`- [ ] I can …`), 3 items, with "Check off each goal once you can do it." Then a **Skills:** line with the rubric skill names.
5. **Quick recall**: 1 to 3 bullets reminding the reader of something they already did that this reading builds on. Start each with "Recall that…". Include a line of code when it helps. Link the earlier page by its title. No module or day numbers.
6. **New tool: <name>** (only when the reading introduces a tool or package). Three parts, nothing more:
   - **What it's for:** 1 or 2 sentences.
   - **How you'll see it in this reading:** the actual lines from the reading in a code block, followed by a **Code walkthrough** (see "Code blocks").
   - **Learn more:** 2 or 3 links: the official docs, and W3Schools when it has a page.
7. **Words to know**: tables of *Word | What it means*. When there are more than 8 terms, split them into small groups. Write each group heading as the plain question, a colon, then the formal name: `### What is typical?: Measures of central tendency`. Under the heading, explain the key plain word ("**Typical** means usual or normal…") and the formal name. Add a *Units* column when the terms are numbers.
8. **Before you read**: no hidden answer. Pick the version that fits:
   - **Scenario:** "In the reading, you'll focus on <scenario>. Think about: <question>. Write down your first answer, then see if the reading agrees."
   - **First answer:** "What's your first answer to <question>? Write it down, then check it against the reading."
   - **Spot the problem** (when the Introduction already covers the idea): "Here's an answer: '<plausible but wrong claim>'. Something is off about it. What? See if the reading agrees with you."
9. **Read**: first "As you read, look for:" with 3 numbered prompts, **then** the reading link and its time.
10. **Main takeaways**:
   - **Summary**: 3 bullets, bold lead-in on each.
   - **Common mix-ups**: table of *If you think… | What's actually true*.
   - **How this connects**: two bullets.
     - **Next reading:** what the reader will *do* next, in plain words, with no undefined tool or function names.
     - **Boss Battle (Module Project):** where this skill shows up, at the skill level only.
11. **Quick check**: 2 questions, answers hidden.
12. **Next**: one link.

### Practice Day and Checkpoint

1. **Title** with its plain name: `Practice Day: Review` or `Module M Checkpoint: Review and Solo Practice`.
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

1. The grouped skills table on the Module Introduction (and the "where you'll practice" table on the Overview)
2. The **Skills:** line on each quest
3. The conclusion's "How to talk about your skills" section

## Checklist before merging a module

- [ ] Every reading URL and "Learn more" link opens.
- [ ] Every relative link and image path resolves.
- [ ] `SUMMARY.md` lists every page in sidebar order, with plain names after a colon and the day in parentheses.
- [ ] No emojis, and no game word without its plain name.
- [ ] No link to a Boss Battle page, and no project deliverables or topics named.
- [ ] No tool or function named before its "New tool" section or "Words to know" entry.
- [ ] Each quest's takeaways match what its reading actually teaches.
- [ ] Each diagram rendered and checked for text size and overlap.
- [ ] No code comment wraps; every code block that teaches something has a Code walkthrough; every parameter is introduced by name.
- [ ] Every page shows its total time at the top.
- [ ] Tool, software, package, module, class, method, attribute, parameter, and argument are used as the "Technical terms" table says.
