# Quest 2.11 — Nobody Was in the Room (Writing for Stakeholders) (Day 12)

**Day 12** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)

**EDA workflow:** Inspect → Clean → Explore → Check → **Explain** ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

The person who acts on your work usually wasn't there when you did it. For example, a coach finds that the team allows most of its goals in the last ten minutes of games. The athletic director won't read the coach's spreadsheet. The director needs the answer, one number, and a picture, in words they can read in one minute.

In this reading, you'll learn how to:

* save a chart as an image file
* write a README page that shows what you found
* write a short data-quality memo that says how much to trust it

**Main takeaway:** Write each page so a reader understands it without your code or your notebook. Start with the answer, give one number, and say what still needs checking.

**Why it matters at work:** The person who makes a decision from your work won't open your notebook. If your finding can't be understood on its own, no one will use it. A clear README is also the first thing an employer sees on your GitHub.

## Learning goals

Check off each goal once you can do it.

- [ ] I can save a chart as an image and embed it in a README with alt text.
- [ ] I can write a README whose sections each stand on their own.
- [ ] I can write a data-quality memo with a plain answer, two checkable questions, and what they'd mean for the decision.

**Skills:** Stakeholder Communication · Data Visualization · Critical Thinking

## Quick recall

* Recall that you saved a chart as an image with `plt.savefig("tradeins_hist.png", dpi=150)`, before `plt.show()`, so you could share just the picture, in [Two Sets of Eyes](quest-10-ai-on-charts.md).
* Recall that you rewrote a vague question like "Why is data missing?" into a checkable one that names a group, a number, or a method, in [The Pattern Isn't the Proof](quest-09-clarifying-questions.md).
* Recall that a chart made for someone else gets a title that states the finding and axes with units, in [Real Numbers, Wrong Story](quest-05-chart-best-practices.md).

## Words to know

### Who you're writing for

| Word | What it means |
| --- | --- |
| **Stakeholder** | The person who will use your finding to make a decision. In the reading, it's the transit manager. |
| **Stakeholder-facing** | Written for a reader who doesn't code. It gives the answer and how sure you are, not the code that found it. |
| **BLUF** | Bottom Line Up Front: lead with the answer, then give one number, then name one thing still worth checking. |

### The two pages

| Word | What it means |
| --- | --- |
| **README** | The landing page of a project: the first page anyone opening the repo sees. It answers "What did you find?" |
| **Takeaways** | The README section with findings in plain words, not code. |
| **Memo** | A short note written for someone who has to make a decision. |
| **Data-quality memo** | A separate short page whose job is trust. It answers "Can I trust it?" It has four parts, every time. |
| **Markdown** | A simple way to format plain text. Symbols like `##` and `-` turn into headings and bullets when GitHub shows the file. READMEs are written in Markdown. |
| **Embed** | Put a picture right inside the page, so readers see the chart instead of a link to it. |
| **Alt text** | Words that describe what a chart shows, for readers who use a screen reader. Never just a file name. |

### New code in this reading

| Word | What it means |
| --- | --- |
| **`os.makedirs("images", exist_ok=True)`** | Makes a folder called `images`. `os` is a module that comes with Python. The parameter `exist_ok` is set to `True`, which means it's OK if the folder already exists, so Python won't stop with an error. |
| **`.unstack()`** | Turns the inner group labels (morning, evening) into columns, so each route gets two bars side by side. |

## Before you read

In the reading, you'll focus on Jordan, who found that Route 12 buses run late in the evening. The transit manager will decide whether to add buses. The manager wasn't there when Jordan ran the numbers and won't open a notebook.

Think about: what does the manager need to see on the page to make that decision? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Why you rerun a number right before you put it in a document.
2. What the `!` does in front of an image link, and why the `images` folder has to be committed.
3. The four parts every data-quality memo has.

**[Start the reading: Nobody Was in the Room →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/stakeholder-communication/reading-1-nobodywasintheroom/)** (about 20 minutes)

## Main takeaways

### Summary

* **Recompute a number right before you cite it,** and copy what the cell prints, not what you remember. Jordan copies 10.3 minutes late, for Route 12's evening trips, straight from the output.
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
| "Linking to the notebook is enough." | The reader won't open it. Each README section has to stand on its own. |
| "Alt text can be the file name." | It should say what the chart shows, like "Route 12's evening bar is far taller than the rest." |
| "A memo is a shorter README." | The memo's job is trust: it asks what could make the finding wrong. |

### How this connects

* **Next:** In the Module 2 Checkpoint (Review and Solo Practice), you'll find a pattern on your own in a dataset you've never seen, then review every skill from this module with self-check questions.
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

**Next:** [Module 2 Checkpoint (Review and Solo Practice) (Days 13–14)](checkpoint.md)
