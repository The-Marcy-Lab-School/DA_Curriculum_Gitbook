# Quest 2.10 — Two Sets of Eyes: Checking AI on Charts (Day 11)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → Explore → **Check** → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

AI (artificial intelligence) tools answer quickly and sound confident, even when part of the answer is wrong. For example, you make a chart of one month's temperatures, with the average for each week. You share it with an AI. It says, "Temperatures rose steadily all month." "Steadily" means each week was warmer than the week before.

But your own numbers, in °F (degrees Fahrenheit), say something else:

* Week 1: 58°F
* Week 2: 63°F
* Week 3: 49°F
* Week 4: 68°F

Week 3 was 63 − 49 = 14°F colder than week 2. So the AI's claim is wrong.

![Two line charts of average temperature by week. Each has an x-axis for the week of the month, 1 to 4, and a y-axis for average temperature in °F, 40 to 80. Left, your numbers: 58, 63, 49, and 68°F. Week 3, in red, was 14°F colder than week 2, but the AI said, "Temperatures rose steadily." Right, what rising steadily would look like: 52, 57, 62, and 67°F, with each week 5°F warmer than the last. That would match the AI's claim.](images/ai-temperature-claim.svg)

**Main takeaway:** An AI can describe a chart wrongly and still sound sure. So check each **claim** against numbers you calculated yourself. A claim is one statement that could be checked, like "Temperatures rose steadily all month." When you share a result, you are responsible for it, not the AI.

**Why it matters at work:** Most analysts now use AI tools to describe charts and suggest new ones. Checking those answers is part of the job. For example, analysts check an AI's answer before they:

* paste its summary of a chart into a report
* use the chart type it suggests for a question
* put its description of a trend on a slide (one page of a presentation) for a meeting

If you share an AI's claim without checking it, a wrong number goes out with your name on it.

## Learning goals

After this reading, you should be able to say:

* I can compute my own numbers and save a chart as an image before I ask an AI about it.
* I can split an AI's answer into separate claims and mark each one right, wrong, or unverifiable.
* I can judge a chart an AI suggests on two counts: whether the chart type fits, and whether its claims match my numbers.

**Skills:** AI as Critic · AI Evaluation · Data Distributions & Shape

## Quick recall

You've checked an AI's answer against a data file before. This reading checks an AI's answer about a chart.

* Recall that one very large value pulls the mean up more than the median, so a mean far above the median is a sign of skew. You saw this with one $5,000 gift in [The Loudest Number](quest-01-descriptive-statistics.md).
* Recall that to see the shape of one number column, you pick a histogram or a boxplot, in [Who's This Chart For?](quest-04-two-kinds-of-charts.md).
* Recall that in [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md), a chatbot said volunteers filled 64 bags. The cleanup log added up to 46. You found the claim, found a real source, compared the two, and then decided.

## Words to know

The examples come from the reading. Devon runs a used-book shop. In a **trade-in**, a customer gives the shop old books in exchange for credit. Devon has data on 10 trade-ins and on the prices of 12 books.

### Checking an AI

| Word | What it means | Example |
| --- | --- | --- |
| **AI critique** | Checking an AI's chart description or chart suggestion against the real numbers before you trust it. | Checking the AI's reply about Devon's trade-in chart against the mean and median |
| **Direction 1** | The AI describes a chart you made. You check whether its read matches the real chart. | The AI says the book prices have "one hump." |
| **Direction 2** | The AI suggests a chart. You check whether the suggestion fits the question and the data. | The AI suggests a bar chart with one bar for every book. |
| **Claim** | One statement that could be checked. An AI sentence is a claim until you check it against the data. | "The mean price is about $9." |
| **Verdict** | Your ruling on one claim: right, wrong, or unverifiable, with the number that settles it. | Right: the mean is $9.17. |
| **Unverifiable** | A claim that nothing you computed can settle. It isn't right or wrong yet. It's unchecked. | "Most books are in good condition." The data has no condition column. |

Computing your own numbers first is the habit from [Looks Right. Is It?](../module-01/quest-10-debugging.md). There, you worked out the expected answer by hand before you ran the code. Here, you work out the numbers before you read the AI's answer.

### Reading the shape

| Word | What it means | Example |
| --- | --- | --- |
| **Right-skewed** | Most values are small, with a long tail to the right. The mean gets pulled above the median. | 9 trade-ins of 2 to 7 books, and 1 of 60 books |
| **Peak** | A high spot on a histogram, where many values bunch together. Two peaks often mean two groups are mixed together in one column. | Book prices bunch at $3 to $5 and at $13 to $16. |

Two groups mixed in one column is the problem you met in [Beneath the Total](quest-08-mining-a-pattern.md). There, Downtown's average mixed screen repairs and battery repairs. The fix is the same: group by the column that might split them.

### Code in this reading

The mean and the median come out in the column's **units**: what the numbers count or measure. For trade-ins, the units are books. For prices, they're dollars. The example uses the 10 trade-ins, sorted: 2, 3, 3, 4, 4, 5, 5, 6, 7, and 60 books.

| Word | What it means | Example |
| --- | --- | --- |
| **`.describe()[["mean", "50%"]]`** | Picks two rows of `describe()`: the mean and the "50%" row, which is the median. | Mean = 99 ÷ 10 = **9.9 books**. Median = (4 + 5) ÷ 2 = **4.5 books**. |
| **`.plot.hist(bins=12)`** | Draws a histogram. The parameter `bins` is set to `12`, so the chart has 12 bars. | A histogram of books brought per trade-in |
| **`plt.savefig("tradeins_hist.png", dpi=150)`** | Saves the chart as an image file. The parameter `dpi` (dots per inch) is set to `150`. A bigger number makes a sharper picture. | Makes the file `tradeins_hist.png` to share with the AI |

{% hint style="info" %}
**Save before you show.** `plt.savefig` must come before `plt.show()`. Showing a chart clears it, so saving after that gives you a blank image.
{% endhint %}

## Before you read

In the reading, you'll focus on Devon, who runs a small used-book shop where customers trade in old books for store credit. **Store credit** is money that can only be spent in that shop. Devon saves a chart of the trade-ins and asks an AI chat to describe it. The AI answers fast and sounds sure.

Think about: what would you need in hand before you could tell whether the AI is right? Write down your first answer, then see if the reading agrees.

## ⭐ Read

As you read, look for:

1. Why you compute your own numbers *before* you read any AI answer.
2. Why a mean and median that are close together don't always mean the data has one hump (one peak).
3. The two counts you judge an AI's chart idea on.

**[Start the reading: Two Sets of Eyes →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/ai-on-charts/reading-1-twosetsofeyes/)** (about 20 minutes)

## Main takeaways

### Summary

* **Get your own numbers first.** Save the chart with `plt.savefig` before `plt.show()`, share only the image with a fresh AI chat, and ask a plain question that doesn't hint at the answer. For the trade-ins, the mean is 9.9 books and the median is 4.5, so the data is right-skewed and the median is the typical trade-in.
* **Split the AI's reply into claims.** Mark each one right, wrong, or unverifiable, and name the number that settles it. An AI is often partly right, so check every claim on its own.
* **Look at the chart, not just the summary numbers.** If the mean lands where almost no data sits, the rows may be two groups mixed together. Group by the column that might split them.

![A flow. Step 1: calculate your own numbers first. Step 2: ask the AI about your chart. Step 3: split its answer into separate claims. Each claim gets a verdict: right (your numbers agree), wrong (your numbers disagree), or unverifiable (nothing you have settles it). Step 4: you decide what to share. Name the number that settles each claim. You are responsible for what you share, not the AI.](images/ai-claim-check.svg)

In the reading's book-price example, Devon has 12 books. Sorted, the prices are $3, $3, $4, $4, $4, $5, $13, $14, $14, $15, $15, and $16. The AI made five claims:

| AI's claim | Verdict | What settles it |
| --- | --- | --- |
| "The mean price is about $9." | Right | The mean is $110 ÷ 12 = $9.17. |
| "The mean and median are close." | Right | The median is the average of the 6th and 7th prices: ($5 + $13) ÷ 2 = $9.00. |
| "Fairly symmetric, with one hump." | Wrong | The histogram has two peaks. The 6 paperbacks (books with soft paper covers) average $23 ÷ 6 = $3.83. The 6 hardcovers (books with stiff covers) average $87 ÷ 6 = $14.50. |
| "$9 is a typical price." | Wrong | $9 sits in the gap between the two groups. No book costs between $5 and $13. |
| "Most books are in good condition." | Unverifiable | The data has no condition column. |

In Direction 2, the AI suggested a bar chart with one bar for every book's price and said hardcovers cost about twice as much as paperbacks. Both fail:

* A histogram fits a question about spread.
* $14.50 ÷ $3.83 = about 3.8. Hardcovers cost almost four times as much, not twice.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The AI sounds sure, so it's probably right." | How sure it sounds tells you nothing. The AI said the book prices have one hump. The histogram has two peaks. Your numbers decide. |
| "The AI got one thing wrong, so I'll ignore all of it." | In the book-price reply, 2 of the 5 claims were right: the mean is about $9, and the mean and median are close. Judge each claim separately. |
| "The mean is close to the median, so the data has one hump in the middle." | The book prices have a mean of $9.17 and a median of $9.00. But no book costs between $5 and $13. Two groups can average out to the middle, so always look at the chart too. |

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

**Next:** [Quest 2.11 — Nobody Was in the Room: Writing for Stakeholders (Day 12)](quest-11-stakeholder-communication.md)
