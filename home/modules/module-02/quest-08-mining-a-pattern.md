# Quest 2.8 — Beneath the Total: Finding Patterns in Groups (Day 9)

**Total time:** about 35 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Sometimes one average hides important differences. For example, two drivers each make 5 deliveries. Sam's take 40 minutes on average, and Alex's take 25 minutes. Sam looks slow.

But the two drivers did different kinds of trips. A **route** is the path a driver follows. A long-route trip outside the city takes 45 minutes. A trip downtown (in the center of the city) takes 20 minutes.

* Sam drove 4 long routes and 1 downtown trip.
* Alex drove 1 long route and 4 downtown trips.

Recall that an average is the sum of the values ÷ the number of values:

* Sam's average = (4 × 45 + 20) ÷ 5 = 200 ÷ 5 = **40 minutes**
* Alex's average = (45 + 4 × 20) ÷ 5 = 125 ÷ 5 = **25 minutes**

On the same route, they are equally fast: both take 45 minutes on a long route and 20 minutes downtown. Sam's average is higher only because Sam drove more long routes.

![Two drivers' deliveries. Left, all deliveries: Sam made 4 long-route deliveries, in red, at 45 minutes each, and 1 downtown delivery, in grey, at 20 minutes. Alex made 1 long-route delivery at 45 minutes and 4 downtown deliveries at 20 minutes. Sam's average = (4 × 45 + 20) ÷ 5 = 200 ÷ 5 = 40 minutes. Alex's average = (45 + 4 × 20) ÷ 5 = 125 ÷ 5 = 25 minutes. Sam looks 15 minutes slower because Sam drove 4 long routes. Right, the same route: on the long route both take 45 minutes, and downtown both take 20 minutes, so on the same route they are equally fast.](images/driver-route-mix.svg)

In this reading, you'll learn how to:

* split a number by two columns at the same time
* check what each group is made of before you compare groups
* tell a real finding apart from one that has another cause, or one that everyone already knows

**Main takeaway:** A gap between two averages can come from a **confound** instead of a real difference. A confound is a pattern that something else explains, like Sam's 4 long routes making Sam look slow. Count what each group is made of, then compare the same kind of row across groups.

**Why it matters at work:** Splitting a number into groups shows what really drives it, before anyone acts on it. For example, teams use it to:

* decide which store, team, or worker needs help
* set fair goals for drivers who work different routes
* plan how many workers each kind of job needs

If you act on a gap that the mix created, you pay for the wrong fix. For example, you might retrain a team that was never slow.

## Learning goals

After this reading, you should be able to say:

* I can split a number by two columns at once to compare every combination.
* I can count what each group is made of before I compare groups, and spot a confound.
* I can tell a finding worth reporting from one that rests on a tiny group or that everyone already knows.

**Skills:** Data Mining · Statistical Analysis

## Quick recall

You've grouped by one column and checked every pair in a nested loop. This reading puts the two ideas together.

* Recall that you turned many rows into one row per group with `drives.groupby("site")["units"].agg(["count", "mean", "median"])` in the interactive reading for [One Row Per Group](quest-03-group-columns.md). Keeping the count next to the mean showed how many rows each number rested on. This reading groups by two columns at once.
* Recall that when a group's mean sits well above its median, a few big values are pulling the mean up, so the median is the better typical value. You saw this in [The Loudest Number](quest-01-descriptive-statistics.md).
* Recall that a nested loop runs its inner body once for every outer pass, in [Trace the Path](../module-01/quest-01-control-flow.md). 3 worlds × 4 checkpoints printed 12 lines. Grouping by two columns gives every combination the same way.

## Words to know

### Splitting a number into groups

The examples use the reading's 12 repairs at FixIt, a phone repair shop with two locations, Downtown and Eastside.

| Word | What it means | Example |
| --- | --- | --- |
| **Segment** | Split a number by one or two columns, so each group gets its own value. Splitting by two columns gives every combination. | Minutes split by shop and repair type: 2 shops × 2 repair types = 4 groups |
| **Mix** | Which kinds of rows make up a group. A group's mix can drive its average. | Downtown: 5 screen repairs and 1 battery repair |
| **`groupby(["shop", "repair"])`** | Groups by two columns at once. Pass a list of columns, and you get one group for each combination. | "Downtown, screen" or "Eastside, battery" |

Each group's label is a pair of values, like `("Downtown", "screen")`. That's a **tuple**, from [Pick the Right Container](../module-01/quest-04-data-structures.md). A tuple is like a list that can't change:

* A list, `["Downtown", "screen"]`, can change: `.append("old")` adds a third value.
* A tuple, `("Downtown", "screen")`, can't change. `.append()` gives an error.

Because a tuple can't change, it can be a dictionary key. Here, it works as each group's key.

### Numbers that describe each group

**Units** are what a number counts or measures. In this table, `.size()`, sample size, and count are in rows (here, repairs). Every other number is in minutes, the same units as the data. The examples use the 3 old-phone screen repairs: 55, 58, and 56 minutes.

| Word | What it means | Example |
| --- | --- | --- |
| **`.size()`** | Counts the rows in each group. | Downtown, screen = **5 repairs** |
| **Sample size** | How many rows a number rests on. In a tiny group, one unusual row can move the average a lot. | Downtown did only **1 battery repair**, too few to trust. |
| **Standard deviation (std)** | How far values usually sit from the mean. A small std means the values are close together. | 55, 58, and 56 sit close together: std = **1.5 minutes** |
| **`.agg(["count", "mean", "median", "std"])`** | Works out several summaries for each group at once, one column each. `"std"` adds the standard deviation. | Count **3 repairs**, mean (55 + 58 + 56) ÷ 3 = **56.3 minutes**, median **56 minutes**, std **1.5 minutes** |

You've seen a small test mislead before. In [When the Crowd Grows](../module-01/quest-03-big-o-intuition.md), a fast test on a few items didn't prove much. The code could still be slow on many. An average from a tiny group is the same: a few rows can't prove a pattern.

### Is the pattern real?

| Word | What it means | Example |
| --- | --- | --- |
| **Confound** | A pattern that is really explained by something else. | The shop seems to matter, but it is standing in for the repair type. |
| **Confounding variable** | The "something else" behind a confound. | The repair type: screen or battery |
| **Non-obvious pattern** | A real, checkable finding that the reader wouldn't have guessed from the obvious groups alone, and that they would act on. | Old phones take about 8 minutes longer for a battery repair. |
| **Simpson's paradox** | When a group looks better or worse overall, but the gap shrinks or flips once you compare the same kind of row. The mix causes it. The reading's optional video shows another example. | Overall, Downtown takes 15.2 minutes longer. For screen repairs, Downtown is 1 minute faster: 50.0 vs. 51.0. |

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

Each shop did 6 repairs. The two averages are:

* Downtown = (55 + 45 + 24 + 58 + 44 + 48) ÷ 6 = 274 ÷ 6 = **45.7 minutes**
* Eastside = (25 + 56 + 17 + 16 + 46 + 23) ÷ 6 = 183 ÷ 6 = **30.5 minutes**

The 15-minute gap came from the mix. 5 of Downtown's 6 repairs were screen repairs, which take longer. Only 2 of Eastside's 6 were. For the same job, the shops take about the same time. The real finding was elsewhere: old phones take about 8 minutes longer for a battery repair and about 10 minutes longer for a screen repair. Because the counts are small, the next step is to check that it holds over more weeks.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Downtown's average is 15 minutes higher, so Downtown is slow." | Downtown did 5 screen repairs and 1 battery repair. Eastside did 2 and 4. For screen repairs alone, Downtown takes 50.0 minutes and Eastside takes 51.0. That's a confound. |
| "I'll always report the median, just to be safe." | Pick the one that fits. In every group in the reading, the mean and median differ by 0.3 minutes or less. The std is 1.7 minutes or less. So the mean is fine. |
| "It's true, so it's a finding." | "Screen repairs take longer" is true, but the owner already knows it. "Old phones take about 8 to 10 minutes longer" is new to the owner, so it's a finding. |

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
