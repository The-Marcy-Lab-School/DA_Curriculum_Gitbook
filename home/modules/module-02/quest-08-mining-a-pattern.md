# Quest 2.8 — Beneath the Total (Day 9)

{% hint style="info" %}
**In one sentence:** One average can hide groups that differ a lot, so split it before you trust it.
{% endhint %}

## Why this matters

Acting on a wrong pattern costs money, like retraining a team that was never slow. Finding a pattern someone *can* act on, and that they didn't already know, is one of the most valuable things an analyst does.

## What you'll be able to do

* I can split a number by two columns at once to compare every combination.
* I can check what each group is made of before I compare groups.
* I can tell a real, non-obvious pattern apart from one caused by something else, or from a fact everyone already knows.

**Skills:** Data Mining · Statistical Analysis

## Words to know

| Word | What it means |
| --- | --- |
| **Segment** | Split a number by one or two columns, so each group gets its own value. |
| **Mix** | Which kinds of rows make up a group. A group's mix can drive its average. |
| **Confound** | Something else that explains a pattern. The thing you're comparing is just standing in for it. |
| **Non-obvious pattern** | A real, checkable finding that the reader wouldn't have guessed. |
| **Standard deviation (std)** | How far values usually sit from the mean. Small means close together. |
| **`.size()`** | Counts the rows in each group. |

## Before you read

A repair shop's Downtown location takes 15 minutes longer per repair, on average, than its Eastside location. The owner asks, "Is Downtown slow?" What would you want to know before you answer?

<details>
<summary>Answer</summary>

Whether the two locations do the same kinds of repairs. If Downtown gets more of the long jobs, its average would be higher even if its workers are just as fast.

</details>

## Read

**[Start the reading: Beneath the Total →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/mining-a-pattern/reading-1-beneath-the-total/)** (about 19 minutes)

As you read, look for:

1. What happens to the 15-minute gap when you compare the same repair type at both shops.
2. Why one of the group averages is too small to trust.
3. What makes the old-phone finding worth telling the owner.

## Main takeaways

### Summary

* **When one group looks much better or worse, count its mix first** with `groupby([...]).size()`, then compare the same kind of row across groups.
* **A finding worth reporting** holds in every group, rests on enough rows, and is something the reader would act on.
* **Use the statistic that fits.** The mean is fine when it's close to the median and the standard deviation is small.

| Comparison | Downtown | Eastside |
| --- | --- | --- |
| All repairs (mean minutes) | 45.7 | 30.5 |
| Mix: screen / battery repairs | 5 / 1 | 2 / 4 |
| Screen repairs only (mean minutes) | 50.0 | 51.0 |

The 15-minute gap came from the mix. Downtown did more screen repairs, which take longer. For the same job, the shops take about the same time.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Downtown's average is higher, so Downtown is slow." | Downtown did more of the long repairs. That's a confound. |
| "Always report the median to be safe." | Pick the one that fits. If the mean and median are close and the std is small, the mean is fine. |
| "Any true statement is a finding." | "Screen repairs take longer" is true, but the owner already knows it. A finding is something they didn't. |

### How this connects

* **Next quest:** A pattern you found still needs questions about where the data came from before anyone acts on it.
* **Checkpoint:** On Day 13, you'll do this on your own with a dataset you've never seen.
* **Boss Battle:** Part 4 asks for a non-obvious finding. Two common ways to lose points: reporting only the overall number, and trusting a pattern from a tiny group.

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

**Next:** [Quest 2.9 — The Pattern Isn't the Proof](quest-09-clarifying-questions.md)
