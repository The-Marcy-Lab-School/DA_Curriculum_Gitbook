# Quest 2.8 — Beneath the Total: Finding Patterns in Groups (Day 9)

**Total time:** about 30 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Sometimes one average hides important differences. For example, Sam's deliveries take 40 minutes on average, and Alex's take 25 minutes. Sam looks slow. But Sam drives a long route outside the city, and Alex delivers downtown. On the same route, they may be equally fast.

In this reading, you'll learn how to:

* split a number by two columns at the same time
* check what each group is made of before you compare groups
* tell a real finding apart from one that has another cause, or one that everyone already knows

**Main takeaway:** One average can hide groups that are very different. Split it into groups before you trust it.

**Why it matters at work:** Acting on a wrong pattern costs money. For example, a company might retrain a team that was never slow. Finding a real pattern that people didn't know, and can act on, is one of the most valuable things an analyst does.

## Learning goals

Check off each goal once you can do it.

- [ ] I can split a number by two columns at once to compare every combination.
- [ ] I can count what each group is made of before I compare groups, and spot a confound.
- [ ] I can tell a finding worth reporting from one that rests on a tiny group or that everyone already knows.

**Skills:** Data Mining · Statistical Analysis

## Quick recall

* Recall that you turned many rows into one row per group with `drives.groupby("site")["units"].agg(["count", "mean", "median"])` in [One Row Per Group](quest-03-group-columns.md). Keeping the count next to the mean showed how many rows each number rested on. This reading groups by two columns at once.
* Recall that when a group's mean sits well above its median, a few big values are pulling the mean up, so the median is the better typical value. You saw this in [The Loudest Number](quest-01-descriptive-statistics.md).

## Words to know

### Splitting a number into groups

| Word | What it means |
| --- | --- |
| **Segment** | Split a number by one or two columns, so each group gets its own value. Splitting by two columns gives every combination. |
| **Mix** | Which kinds of rows make up a group. A group's mix can drive its average. |
| **`groupby(["shop", "repair"])`** | Groups by two columns at once. Pass a list of columns, and you get one group for each combination, like "Downtown, screen" or "Eastside, battery." |

### Numbers that describe each group

| Word | What it means | Units |
| --- | --- | --- |
| **`.size()`** | Counts the rows in each group. | Rows |
| **Sample size** | How many rows a number rests on. In a tiny group, one unusual row can move the average a lot. | Rows |
| **Standard deviation (std)** | How far values usually sit from the mean. A small std means the values are close together. | Same as the data (here, minutes) |
| **`.agg(["count", "mean", "median", "std"])`** | Works out several summaries for each group at once, one column each. `"std"` adds the standard deviation. | Count is in rows. The others are in the data's units (minutes). |

### Is the pattern real?

| Word | What it means |
| --- | --- |
| **Confound** | A pattern that is really explained by something else. In the reading, the shop seems to matter, but it is standing in for the repair type. |
| **Confounding variable** | The "something else" behind a confound. In the reading, it's the repair type. |
| **Non-obvious pattern** | A real, checkable finding that the reader wouldn't have guessed from the obvious groups alone, and that they would act on. |
| **Simpson's paradox** | When a group looks better or worse overall, but the gap shrinks or flips once you compare the same kind of row. The mix causes it. The reading's optional video shows an example. |

{% hint style="info" %}
**Ask what else is different about the group.** Before you blame a shop, a team, or a person for a gap, count each group's mix. Naming what else differs between groups is the habit that catches a confound.
{% endhint %}

## Before you read

In the reading, you'll focus on FixIt, a phone repair shop with two locations. Downtown repairs take about 15 minutes longer on average than Eastside repairs, and the owner asks, "Is Downtown slow?"

Think about: what would you want to know before you answer? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. What happens to the 15-minute gap when you compare the same repair type at both shops.
2. Why one of the group averages is too small to trust.
3. What makes the old-phone finding worth telling the owner, when "screen repairs take longer" isn't.

**[Start the reading: Beneath the Total →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/mining-a-pattern/reading-1-beneath-the-total/)** (about 20 minutes)

## Main takeaways

### Summary

* **Count the mix before you compare groups.** When one group looks much better or worse, run `groupby([...]).size()` to see what each group is made of. Then compare the same kind of row across groups.
* **A finding worth reporting** is real, checkable, and something the reader would act on. It holds in every group and rests on enough rows. "Screen repairs take longer" is true, but the owner already knows it.
* **Use the statistic that fits.** The mean is fine when it's close to the median and the std is small. In the reading, that's true in every group, so the mean backs up the finding.

![Two bar charts of FixIt's repair times, with a y-axis of average minutes. Left, all repairs: Downtown 45.7 minutes and Eastside 30.5, about 15 minutes apart. Right, screen repairs only: Downtown 50.0 and Eastside 51.0, about the same. Downtown did 5 screen repairs and 1 battery repair. Eastside did 2 and 4. Screen repairs take longer.](images/confound-gap.svg)

The 15-minute gap came from the mix. Downtown did more screen repairs, which take longer. For the same job, the shops take about the same time. The real finding was elsewhere: old phones take about 8 minutes longer for a battery repair and about 10 minutes longer for a screen repair. Because the counts are small, the next step is to check that it holds over more weeks.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Downtown's average is higher, so Downtown is slow." | Downtown did more of the long repairs. That's a confound. |
| "Always report the median to be safe." | Pick the one that fits. If the mean and median are close and the std is small, the mean is fine. |
| "Any true statement is a finding." | "Screen repairs take longer" is true, but the owner already knows it. A finding is something they didn't. |

### How this connects

* **Next reading:** You'll take a pattern like this and question the data behind it: who collected it, what's missing, and which groups got counted less. Then you'll write questions specific enough that the person who looks after the data could answer them.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll look for a non-obvious finding in a real dataset. Before you report a gap between groups, you'll check each group's mix and size, and compare the same kind of row across groups.

## Quick check

**1.** Next month, Eastside's average repair time is 12 minutes higher than Downtown's. The owner wants to move a worker. What do you check first?

<details>
<summary>Answer</summary>

The mix. Run `groupby(["shop", "repair"]).size()` to see whether Eastside got more screen repairs, then compare the same repair type across shops.

</details>

**2.** "Downtown's battery repairs are slower than Eastside's," based on 1 Downtown battery repair. Report it?

<details>
<summary>Answer</summary>

Not yet. One repair is too few to trust. Check it with more data first.

</details>

---

**Next:** [Quest 2.9 — The Pattern Isn't the Proof: Asking Questions About Your Data (Day 10)](quest-09-clarifying-questions.md)
