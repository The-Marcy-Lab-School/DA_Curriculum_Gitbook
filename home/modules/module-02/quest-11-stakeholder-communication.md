# Quest 2.11 — Nobody Was in the Room: Writing for Stakeholders (Day 12)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → Explore → Check → **Explain** ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

The person who acts on your work usually wasn't there when you did it. For example, a coach looks at a spreadsheet of every game this season. The team allowed 20 goals (let the other team score 20 times). 12 of those 20 came in the last 10 minutes of games.

The athletic director (the person in charge of a school's sports teams) won't read the coach's spreadsheet. The director needs the answer, one number, and a picture, in words they can read in one minute. For example: "Most goals against us come late in games: 12 of 20 came in the last 10 minutes."

**Main takeaway:** A **stakeholder** is the person who uses your finding to make a decision. They need a page that makes sense without your code or your notebook. Start with the answer, give one number, and say what still needs checking. This order is called **BLUF**: Bottom Line Up Front.

**Why it matters at work:** Writing for stakeholders is how your analysis turns into a decision. For example, analysts write short pages to:

* tell a manager which bus route needs more buses
* show a director (the person who runs a department) why sales dropped last month
* explain a project on GitHub to an employer who might hire you

If the page only makes sense with your notebook open, no one will use your finding.

## Learning goals

After this reading, you should be able to say:

* I can save a chart as an image and embed it in a README with alt text.
* I can write a README whose sections each make sense without my notebook.
* I can write a data-quality memo with a plain answer, two checkable questions, and what they'd mean for the decision.

**Skills:** Stakeholder Communication · Data Visualization · Critical Thinking

## Quick recall

You've saved charts, written checkable questions, and pushed work to GitHub. This reading uses them together to write for a reader.

* Recall that you saved a chart as an image with `plt.savefig("tradeins_hist.png", dpi=150)`, before `plt.show()`, so you could share just the picture, in [Two Sets of Eyes](quest-10-ai-on-charts.md).
* Recall that you rewrote a vague question like "Why is data missing?" into a checkable one that names a group, a number, or a method, in [The Pattern Isn't the Proof](quest-09-clarifying-questions.md).
* Recall that `git add` stages a file and `git commit` saves it. A commit isn't on GitHub until you `git push`. You did this in [Save the Story of Your Work](../module-00/quest-03-git.md). A README and its chart images go through the same steps.

## Words to know

The examples come from the reading. Jordan found that Route 12 buses run late in the evening, and writes it up for the transit manager.

### Who you're writing for

| Word | What it means | Example |
| --- | --- | --- |
| **Stakeholder** | The person who will use your finding to make a decision. | The transit manager: the person who runs the city's buses |
| **Stakeholder-facing** | Written for a reader who doesn't code. It gives the answer and how sure you are, not the code that found it. | "Route 12 evening trips run about 10 minutes late," not `trips.groupby(...)` |
| **BLUF** | Bottom Line Up Front. The "bottom line" is your main answer. Lead with the answer, then give one number, then name one thing still worth checking. | Route 12 is late in the evening. → 10.3 minutes late. → Were canceled trips left out? |

### The two pages

| Word | What it means | Example |
| --- | --- | --- |
| **README** | The landing page of a project: the first page anyone opening the repo (repository, the project's folder on GitHub) sees. It answers "What did you find?" | Jordan's `README.md`, titled "Route 12 Evening Delays" |
| **Takeaways** | The README section with findings in plain words, not code. | "Morning trips on both routes run close to on time." |
| **Memo** | A short note written for someone who has to make a decision. | A note to the transit manager |
| **Data-quality memo** | A separate short page whose job is trust. It answers "Can I trust it?" It has four parts, every time. | Jordan's memo asks, "Were canceled Route 12 evening trips left out of the file?" |
| **Markdown** | A simple way to format plain text. Symbols like `##` and `-` turn into headings and bullets when GitHub shows the file. READMEs are written in Markdown. | `## Takeaways` shows as a heading. |
| **Embed** | Put a picture right inside the page, so readers see the chart instead of a link to it. | `![alt text](images/late_by_route.png)` |
| **Alt text** | Words that describe what a chart shows, for readers who use a screen reader (a program that reads the screen out loud). Never just a file name. | "Route 12's evening bar is more than three times taller than any other bar." |

You've seen a README before. In [Meet Your Terminal](../module-00/quest-01-terminal.md), `ls` listed a `README.md` file in the `garden` folder. The `.md` at the end means it's written in Markdown.

### New code in this reading

| Word | What it means | Example |
| --- | --- | --- |
| **`os.makedirs("images", exist_ok=True)`** | Makes a folder called `images`. `os` is a module that comes with Python. The parameter `exist_ok` is set to `True`, which means it's OK if the folder already exists, so Python won't stop with an error. | Makes `images/` next to `README.md`, where the chart is saved |
| **`.unstack()`** | Turns the inner group labels (morning, evening) into columns, so each route (the path one bus line follows) gets two bars side by side. | See the before and after below. |

In the reading, `means` holds the average minutes late for each route and time of day. It's a Series, one column of values with labels. Each label has two parts, like `Route 12, evening`. `.unstack()` turns it into a small table, with the times of day as columns.

Before, `means` is a Series with 4 rows:

| Label | Minutes late |
| --- | --- |
| Route 12, evening | 10.3 |
| Route 12, morning | 2.0 |
| Route 7, evening | 3.0 |
| Route 7, morning | 1.0 |

After, `means.unstack()` is a table with 2 rows and 2 columns:

| Route | evening | morning |
| --- | --- | --- |
| Route 12 | 10.3 | 2.0 |
| Route 7 | 3.0 | 1.0 |

A bar chart of the table draws one group of bars per row. So each route gets an evening bar and a morning bar.

The README finds its chart by a **relative path**, like `images/late_by_route.png`. You used relative paths with `cd` in [Meet Your Terminal](../module-00/quest-01-terminal.md). This one starts from the folder that holds the README.

## Before you read

In the reading, you'll focus on Jordan, who found that Route 12 buses run late in the evening. The transit manager will decide whether to add buses. The manager wasn't there when Jordan ran the numbers and won't open a notebook.

Think about: what does the manager need to see on the page to make that decision? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. Why you rerun a number right before you put it in a document.
2. What the `!` does in front of an image link, and why the `images` folder has to be committed.
3. The four parts every data-quality memo has.

**[Start the reading: Nobody Was in the Room →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/stakeholder-communication/reading-1-nobodywasintheroom/)** (about 20 minutes)

## Main takeaways

### Summary

* **Recompute a number right before you cite it (use it in your writing),** and copy what the cell prints, not what you remember. Jordan copies 10.3 minutes late, for Route 12's evening trips, straight from the output. Route 12's three evening trips were 9, 12, and 10 minutes late: (9 + 12 + 10) ÷ 3 = 31 ÷ 3 = 10.3 minutes.
* **Save the chart as a file, then embed it.** Make an `images` folder, save the chart with `plt.savefig` before `plt.show()`, and embed it with `![alt text](images/name.png)`. Commit the `images` folder along with the README, or the picture won't show up on GitHub.
* **Two pages, two jobs.** The README says what you found, in the sections the project asks for. The data-quality memo says how far to trust it, in four parts.

![Your finding starts in your notebook, which the stakeholder won't open. It becomes two pages. The README answers "What did you find?": the answer first in plain words, one key number, and an embedded chart with alt text. The data-quality memo answers "Can I trust it?" in four parts: domain and stakeholder on one line, your answer in one sentence with no code words, two checkable questions about the data, and whether a bad answer would change your advice.](images/two-pages.svg)

Every README is built from the same five Markdown pieces:

| To make... | Write |
| --- | --- |
| A section heading | `## Takeaways` |
| A bullet | `- Route 12 evening trips run about 10 minutes late.` |
| A bold key number | `**10.3 minutes**` |
| A link to the data | `[Bus tracking data](data/trips.csv)` |
| An embedded chart | `![Bar chart of average minutes late by route](images/late_by_route.png)` |

Without the `!`, GitHub shows a plain link instead of the picture.

{% hint style="info" %}
**Don't skip the memo's last line.** "Does this affect trust?" says whether a bad answer to one of your questions would change your advice. It's the line people most often leave out, and it tells the stakeholder what your questions mean for the decision.
{% endhint %}

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "I'll just link to my notebook, so the manager can see the results." | The manager won't open it. Write the finding right in the README: "Route 12 evening trips run about 10 minutes late." |
| "The file name, `late_by_route.png`, is fine for alt text." | Alt text says what the chart shows: "Route 12's evening bar is more than three times taller than any other bar." Its 10.3 minutes is 3.4 times the next tallest bar, 3.0 minutes. |
| "The memo is just a shorter README." | The memo's job is trust: it asks what could make the finding wrong. For example: "Were canceled Route 12 evening trips left out of the file, or counted as late?" |

### How this connects

* **Next:** In the Module 2 Checkpoint: Review and Solo Practice, you'll find a pattern on your own in a dataset you've never seen, then review every skill from this module with self-check questions.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll explain your finding in writing to someone who won't read your code. You'll lead with the answer, embed a chart with alt text that says what it shows, and name what's still worth checking before anyone acts on it.

## Quick check

**1.** Which alt text helps a reader who can't see the chart?

* A. `late_by_route.png`
* B. "Route 12 runs late on evening trips"
* C. "Bar chart of average minutes late by route, morning and evening. Route 12's evening bar is far taller than the rest."

<details>
<summary>Answer</summary>

**C.** It says what kind of chart it is and what it shows. A is a file name, and B is a title, not a description.

</details>

**2.** Your saved chart image is blank. What's the most likely cause?

<details>
<summary>Answer</summary>

`plt.savefig` came after `plt.show()`. Showing a chart clears it, so save first.

</details>

---

**Next:** [Module 2 Checkpoint: Review and Solo Practice (Days 13–14)](checkpoint.md)
