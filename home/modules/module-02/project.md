# Module 2 Boss Battle (Project): Exploratory Data Analysis (Days 15–19)

{% hint style="info" %}
**In one sentence:** Pick a real-world topic, then inspect, clean, explore, check, and explain its data for a stakeholder who needs an answer they can trust.
{% endhint %}

## Why this matters

Most of an analyst's time goes into understanding and cleaning data before any answer is trustworthy. This project is your first full pass through that work, with every decision explained. It's also a portfolio piece: a public GitHub repo an employer can open and read.

## What you'll build

* **A Jupyter notebook** that inspects and cleans messy data, adds a new column, profiles key columns with statistics and charts, and finds a non-obvious pattern across groups.
* **Two AI checks:** you judge an AI's read of your chart, and you judge a chart an AI suggests.
* **A data-quality memo** (`memo.md`) for your stakeholder: your answer and 2 checkable questions about the data.
* **Your own README**, written for an employer, with at least one embedded chart.
* **A 3–5 minute share-out** on Day 19, from a short slide deck.

The official checklist and rubric are in `CHECKLIST_RUBRIC.md` in your project repo. Your instructor will share the link to the project template.

## Choose your topic

Pick **one**. Everyone uses the same notebook and requirements.

| Topic | Stakeholder | Their question | Suggested new column |
| --- | --- | --- | --- |
| **Finance & Insurance** | An analyst at FEMA's flood insurance program | What does a typical claim actually pay, and are a few huge claims distorting the number? | `total_paid` |
| **Healthcare Operations** | A hospital-quality policy analyst | What does a "typical" psychiatric patient wait look like, and which states and hospitals are outliers? | `over_4_hours` |
| **Public Sector** | A program manager at San Francisco's building department | How long does a permit take, how much does the work cost, and are a few huge projects skewing the story? | `days_to_issue` |
| **Professional Services** | A managing partner at a consulting firm | How do billed hours break down across service lines and partners, and does the timesheet data have gaps? | `is_ongoing` |

Before you write code, write at least 2 **QAR notes** in `REFLECTION.md`:

* **Question:** What does your code need to decide that the stakeholder didn't say? (For example, what counts as "slow"?)
* **Assumption:** What will you assume for now?
* **Risk:** What goes wrong if you're wrong, and how would you check?

## Your sprint, day by day

Start each build day with a 2-minute check-in: What did I finish last time? What will I finish today? Is anything blocking me?

| Day | Goal | What you'll do | Practiced in |
| --- | --- | --- | --- |
| **15** | Set up, choose, inspect | Create your repo from the template, pick a topic, read `data/SOURCE.md`, write QAR notes, and run the four checks (Part 1) | Quests 2.2, 2.9 |
| **16** | Clean, add a column, profile | Write a cleaning function and call it twice, make a drop/fill/flag decision, add a new column, and profile 3 numeric columns (Parts 2–3) | Quests 2.1, 2.3, 2.6, 2.7 |
| **17** | Find a pattern, check the AI | Build a `groupby` comparison and find a non-obvious pattern (Part 4), then do both AI checks (Parts 5 and 5b). Have at least 4 commits pushed by end of day. | Quests 2.8, 2.10 |
| **18** | Answer and write it up | Answer the stakeholder (Part 6), explain your standard deviation (Part 7), write the memo and README, clean up the notebook, run Restart & Run All, and build your deck | Quests 2.1, 2.11 |
| **19** | Share-out | Present for 3–5 minutes to a small group, then take 2 minutes of questions | — |

## How it's graded

You're graded on 10 skills. Meeting the bar on each is worth 3 points (30 total). Doing that skill's **Above & Beyond** item on top of Meets raises it to Exceeds, worth 4 points (40 total possible).

| Skill | What "Meets" looks like |
| --- | --- |
| **Statistical Analysis** | You explain your key number and its standard deviation in terms of your stakeholder's question. |
| **Data Distributions & Shape** | You profile 3 columns, and your shape and outlier calls match your charts. |
| **Data Mining** | You report a non-obvious pattern that rests on enough rows. |
| **Data Cleaning & Imputation** | You write a reusable cleaning function and justify your missing-value decision. |
| **Data Visualization** | Each chart type fits its question, and your README shows real chart images. |
| **Critical Thinking** | You do both AI checks for real, and your memo asks 2 specific, checkable questions. |
| **Stakeholder Communication** | Your README is fully rewritten, with every section the template lists and an embedded chart. |
| **AI as Critic** | You upload your chart, paste the AI's read word for word, and judge each claim against your numbers. |
| **AI Evaluation** | You judge an AI-suggested chart for both chart-type fit and accuracy. |
| **Presentations** | Your deck has every required slide, with the answer right after the title, and your talk opens with the finding. |

## Traps to avoid

These are the most common ways to lose points:

1. Calling a column "normal" or "symmetric" without looking at a chart.
2. Using the mean on clearly skewed data without saying why. This is the most common mistake on record.
3. Trusting a pattern from a very small group.
4. Writing memo questions too vague to check, like "Is this data accurate?"
5. Copy-pasting the same cleaning fix 2 or 3 times instead of writing one function.
6. Filling blanks with no stated reason.
7. Dropping matching rows without checking whether they're really the same record.
8. Computing statistics before handling placeholder or impossible values.
9. Leaving the template's README in place, or describing a chart in words instead of embedding it.
10. Reporting only the overall number, or only the most extreme group.
11. Using a histogram or bar chart for everything, whatever the question.

## Before you submit

* [ ] The notebook runs top to bottom with **Restart & Run All**.
* [ ] Every instruction block and `TODO` is deleted, so the notebook reads like your own finished analysis.
* [ ] `memo.md`, `REFLECTION.md`, and your own `README.md` are done, with at least one embedded chart.
* [ ] School-facing files are deleted, and `starter/` is renamed to `project/`.
* [ ] `project/presentation.pdf` is pushed.
* [ ] You have at least 4 commits with clear messages.
* [ ] Your repo is public, and the chart shows in the README when you open it in a private browser window.

---

**When you're done:** [Module 2 Wrap-Up](wrap-up.md)
