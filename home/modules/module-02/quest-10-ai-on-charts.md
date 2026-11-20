# Quest 2.10 — Two Sets of Eyes (Day 11)

{% hint style="info" %}
**In one sentence:** An AI can describe a chart fast and sound sure while getting part of it wrong, so you check each claim against numbers you computed yourself.
{% endhint %}

## Why this matters

AI tools are now part of most analysts' work. But the person who shares a result is responsible for it, not the tool. Knowing how to check an AI's read of a chart, and its chart ideas, is a skill employers are starting to ask about.

## What you'll be able to do

* I can compute my own numbers and save a chart as an image before I ask an AI about it.
* I can split an AI's answer into separate claims and mark each one right, wrong, or unverifiable.
* I can judge a chart an AI suggests on two counts: whether the chart type fits, and whether its claims match my numbers.

**Skills:** AI as Critic · AI Evaluation · Data Distributions & Shape

## Words to know

| Word | What it means |
| --- | --- |
| **AI critique** | Checking an AI's chart description or chart idea against the real numbers before you trust it. |
| **Direction 1** | The AI describes a chart you made. You check whether its read matches. |
| **Direction 2** | The AI suggests a chart. You check whether it fits the question and the data. |
| **Claim** | One statement that can be checked. |
| **Unverifiable** | A claim nothing you computed can settle. It isn't right or wrong yet. It's unchecked. |
| **Right-skewed** | Most values are small, with a long tail to the right. The mean gets pulled above the median. |
| **`plt.savefig`** | Saves a chart as an image file. Call it before `plt.show()`. |

## Before you read

An AI looks at your chart and says, "The data looks roughly symmetric. The mean is a good typical number." Your numbers show a mean of 9.9 and a median of 4.5. Do you trust it?

<details>
<summary>Answer</summary>

No. A mean that far above the median means the data is right-skewed, not symmetric. The median, 4.5, is the better typical number.

</details>

## Read

**[Start the reading: Two Sets of Eyes →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/ai-on-charts/reading-1-twosetsofeyes/)** (about 19 minutes)

As you read, look for:

1. Why you compute your own numbers *before* you read any AI answer.
2. Why a mean and median that are close together don't always mean the data has one hump.
3. The two counts you judge an AI's chart idea on.

## Main takeaways

### Summary

* **Get your own numbers first.** Save the chart with `plt.savefig` before `plt.show()`, upload only the image, and ask a plain question that doesn't hint at the answer.
* **Split the AI's reply into claims.** Mark each one right, wrong, or unverifiable, and name the number that settles it. An AI is often partly right, so check every claim on its own.
* **Look at the chart, not just the summary numbers.** If the mean lands where almost no data sits, the rows may be two groups mixed together. Group by the column that might split them.

Here's how the reading's book-price example sorts out. The AI said:

| AI's claim | Verdict | What settles it |
| --- | --- | --- |
| "The mean price is about $9." | Right | The mean is $9.17. |
| "The mean and median are close." | Right | The median is $9.00. |
| "Fairly symmetric, with one hump." | Wrong | The histogram has two peaks: paperbacks near $4 and hardcovers near $14.50. |
| "$9 is a typical price." | Wrong | Almost no book costs $9. |
| "Most books are in good condition." | Unverifiable | The data has no condition column. |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The AI sounds sure, so it's probably right." | How sure it sounds tells you nothing. Your numbers decide. |
| "The AI got one thing wrong, so ignore all of it." | It's often partly right. Judge each claim separately. |
| "Mean close to median means one hump in the middle." | Two groups can average out to the middle. Always look at the chart too. |

### How this connects

* **Next quest:** You'll write up a finding for a stakeholder who will never open your notebook.
* **Boss Battle:** In Part 5, you'll paste an AI's read of your own chart word for word and judge each claim. In Part 5b, you'll ask an AI to suggest a chart and judge its type and its claims.

## Quick check

**1.** An AI suggests "a bar chart with one bar for every book's price" to show how prices are spread out. Does the chart type fit?

<details>
<summary>Answer</summary>

No. The question is about one column's shape, so a histogram fits. A bar for every book makes the spread hard to see.

</details>

**2.** Next month's mean is 6.1 and the median is 5.9. The histogram shows one hump with no long tail. An AI says, "Roughly symmetric. The mean is a fine typical number." What do you do?

<details>
<summary>Answer</summary>

Accept both claims. Your numbers and your chart back them up. Checking means agreeing when the evidence agrees, too.

</details>

---

**Next:** [Quest 2.11 — Nobody Was in the Room](quest-11-stakeholder-communication.md)
