# Quest 2.10 — Two Sets of Eyes (Checking AI on Charts)

**Day 11** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)

**EDA workflow:** Inspect → Clean → Explore → **Check** → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

AI tools answer quickly and sound confident, even when part of the answer is wrong. For example, you share a chart of daily temperatures for one month with an AI. It says, "Temperatures rose steadily all month." But your own numbers show a cold week in the middle of the month.

In this reading, you'll learn how to check two things against numbers you calculated yourself:

* an AI's description of a chart you made
* a chart that an AI suggests

**Main takeaway:** Calculate your own numbers first. Then check each AI claim one at a time. When you share a result, you are responsible for it, not the AI.

**Why it matters at work:** Most analysts now use AI tools. Employers are starting to ask whether you can check an AI's description of a chart and judge its chart ideas.

## Learning goals

Check off each goal once you can do it.

- [ ] I can compute my own numbers and save a chart as an image before I ask an AI about it.
- [ ] I can split an AI's answer into separate claims and mark each one right, wrong, or unverifiable.
- [ ] I can judge a chart an AI suggests on two counts: whether the chart type fits, and whether its claims match my numbers.

**Skills:** AI as Critic · AI Evaluation · Data Distributions & Shape

## Quick recall

* Recall that one very large value pulls the mean up more than the median, so a mean far above the median is a sign of skew. You saw this with one $5,000 gift in [The Loudest Number](quest-01-descriptive-statistics.md).
* Recall that to see the shape of one number column, you pick a histogram or a boxplot, in [Who's This Chart For?](quest-04-two-kinds-of-charts.md).
* Recall that a confident AI answer still needs evidence before you use it, in [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md).

## Words to know

### Checking an AI

| Word | What it means |
| --- | --- |
| **AI critique** | Checking an AI's chart description or chart suggestion against the real numbers before you trust it. |
| **Direction 1** | The AI describes a chart you made. You check whether its read matches the real chart. |
| **Direction 2** | The AI suggests a chart. You check whether the suggestion fits the question and the data. |
| **Claim** | One statement that could be checked. An AI sentence is a claim until you check it against the data. |
| **Verdict** | Your ruling on one claim: right, wrong, or unverifiable, with the number that settles it. |
| **Unverifiable** | A claim that nothing you computed can settle. It isn't right or wrong yet. It's unchecked. |

### Reading the shape

| Word | What it means |
| --- | --- |
| **Right-skewed** | Most values are small, with a long tail to the right. The mean gets pulled above the median. |
| **Peak** | A high spot on a histogram, where many values bunch together. Two peaks often mean two groups are mixed together in one column. |

### Code in this reading

| Word | What it means |
| --- | --- |
| **`.describe()[["mean", "50%"]]`** | Picks two rows of `describe()`: the mean and the "50%" row, which is the median. Both come out in the column's units, like books per trade-in or dollars. |
| **`.plot.hist(bins=12)`** | Draws a histogram. The parameter `bins` is set to `12`, so the chart has 12 bars. |
| **`plt.savefig("tradeins_hist.png", dpi=150)`** | Saves the chart as an image file. The parameter `dpi` (dots per inch) is set to `150`. A bigger number makes a sharper picture. |

{% hint style="info" %}
**Save before you show.** `plt.savefig` must come before `plt.show()`. Showing a chart clears it, so saving after that gives you a blank image.
{% endhint %}

## Before you read

In the reading, you'll focus on Devon, who runs a small used-book shop where customers trade in old books for store credit. Devon saves a chart of the trade-ins and asks an AI chat to describe it. The AI answers fast and sounds sure.

Think about: what would you need in hand before you could tell whether the AI is right? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Why you compute your own numbers *before* you read any AI answer.
2. Why a mean and median that are close together don't always mean the data has one hump.
3. The two counts you judge an AI's chart idea on.

**[Start the reading: Two Sets of Eyes →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/ai-on-charts/reading-1-twosetsofeyes/)** (about 20 minutes)

## Main takeaways

### Summary

* **Get your own numbers first.** Save the chart with `plt.savefig` before `plt.show()`, share only the image with a fresh AI chat, and ask a plain question that doesn't hint at the answer. For the trade-ins, the mean is 9.9 books and the median is 4.5, so the data is right-skewed and the median is the typical trade-in.
* **Split the AI's reply into claims.** Mark each one right, wrong, or unverifiable, and name the number that settles it. An AI is often partly right, so check every claim on its own.
* **Look at the chart, not just the summary numbers.** If the mean lands where almost no data sits, the rows may be two groups mixed together. Group by the column that might split them.

Here's how the reading's book-price example sorts out. The AI said:

| AI's claim | Verdict | What settles it |
| --- | --- | --- |
| "The mean price is about $9." | Right | The mean is $9.17. |
| "The mean and median are close." | Right | The median is $9.00. |
| "Fairly symmetric, with one hump." | Wrong | The histogram has two peaks: paperbacks average $3.83 and hardcovers average $14.50. |
| "$9 is a typical price." | Wrong | $9 sits in the gap between the two groups, where no book is priced. |
| "Most books are in good condition." | Unverifiable | The data has no condition column. |

In Direction 2, the AI suggested a bar chart with one bar for every book's price and said hardcovers cost about twice as much as paperbacks. Both fail: a histogram fits a question about spread, and $14.50 is almost four times $3.83, not twice.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The AI sounds sure, so it's probably right." | How sure it sounds tells you nothing. Your numbers decide. |
| "The AI got one thing wrong, so ignore all of it." | It's often partly right. Judge each claim separately. |
| "Mean close to median means one hump in the middle." | Two groups can average out to the middle. Always look at the chart too. |

### How this connects

* **Next reading:** You'll take a finding from your notebook and write it up for a manager who will never open it: one short page that says what you found, with your chart in it, and one that says how far to trust it.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll ask an AI to describe one of your own charts and to suggest a chart. Then you'll judge each claim against numbers you computed yourself, and name the number that settles it.

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

**Next:** [Quest 2.11 — Nobody Was in the Room (Writing for Stakeholders)](quest-11-stakeholder-communication.md)
