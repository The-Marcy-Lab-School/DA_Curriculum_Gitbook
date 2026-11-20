# Quest 2.11 — Nobody Was in the Room (Day 12)

{% hint style="info" %}
**In one sentence:** Turn your notebook finding into two short pages: a README that says what you found, and a memo that says how far to trust it.
{% endhint %}

## Why this matters

The person who makes a decision from your work usually wasn't there when you did it, and they won't open your notebook. If your finding doesn't stand on its own, it doesn't get used. A clear README is also what an employer sees first when they open your GitHub.

## What you'll be able to do

* I can save a chart as an image and embed it in a README with alt text.
* I can write a README whose sections each stand on their own.
* I can write a data-quality memo with a plain answer, two checkable questions, and what they'd mean for the decision.

**Skills:** Stakeholder Communication · Data Visualization · Critical Thinking

## Words to know

| Word | What it means |
| --- | --- |
| **Stakeholder** | The person who will use your finding to make a decision. |
| **Stakeholder-facing** | Written for a reader who doesn't code: the answer and how sure you are, not the code. |
| **README** | A project's landing page. It answers "What did you find?" |
| **Data-quality memo** | A short page whose job is trust. It answers "Can I trust it?" |
| **Takeaways** | The README section with findings in plain words. |
| **Alt text** | Words that describe what a chart shows, for readers using a screen reader. |
| **BLUF** | Bottom Line Up Front: lead with the answer. |

## Before you read

A teammate's README says only "See the notebook for results" under Takeaways. What's wrong with that?

<details>
<summary>Answer</summary>

The manager won't open the notebook, so they're left with nothing. The finding itself needs to be written right there, in plain words.

</details>

## Read

**[Start the reading: Nobody Was in the Room →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/stakeholder-communication/reading-1-nobodywasintheroom/)** (about 19 minutes)

As you read, look for:

1. Why you rerun a number right before you put it in a document.
2. What the `!` does in front of an image link, and why the `images` folder has to be committed.
3. The four parts every data-quality memo has.

## Main takeaways

### Summary

* **Recompute a number right before you cite it,** and copy what the cell prints, not what you remember.
* **Save the chart into an `images` folder** with `plt.savefig` before `plt.show()`, then embed it with `![alt text](images/name.png)`. Commit the folder too.
* **Two pages, two jobs.** The README says what you found, in the sections the project asks for. The memo says how far to trust it, in four parts.

| | README | Data-quality memo |
| --- | --- | --- |
| Answers | "What did you find?" | "Can I trust it?" |
| Includes | Your scenario, data, numbers, an embedded chart, and takeaways in plain words | Domain and stakeholder, a one-sentence answer, 2 checkable questions, and whether a bad answer would change your advice |

Every README uses the same five Markdown pieces:

| To make... | Write |
| --- | --- |
| A section heading | `## Takeaways` |
| A bullet | `- Route 12 runs late in the evening` |
| A bold key number | `**10.3 minutes**` |
| A link | `[Bus data](data/trips.csv)` |
| An embedded chart | `![Bar chart of minutes late by route](images/late_by_route.png)` |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Linking to the notebook is enough." | The reader won't open it. Each README section has to stand on its own. |
| "Alt text can be the file name." | It should say what the chart shows, like "Route 12's evening bar is far taller than the rest." |
| "A memo is a shorter README." | The memo's job is trust: it asks what could make the finding wrong. |

### How this connects

* **Next:** The Checkpoint (Days 13–14), where you find a pattern on your own and review the whole module.
* **Boss Battle:** You'll replace the template's README with your own, embed at least one chart, and write `memo.md`. Your share-out deck starts with a BLUF slide taken straight from your memo's first line.

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

**Next:** [Module 2 Checkpoint](checkpoint.md)
