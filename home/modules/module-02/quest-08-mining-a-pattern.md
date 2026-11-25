# Quest 2.8 — Beneath the Total: Finding Patterns in Groups (Day 9)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Quick recall

You've grouped by one column and checked every pair in a nested loop. This reading puts the two ideas together.

* In the interactive reading for [One Row Per Group](quest-03-group-columns.md), `drives.groupby("site")["units"].agg(["count", "mean", "median"])` gave one row per group. The count next to the mean showed how many rows were used to work out that mean.
* When a group's mean sits well above its median, a few big values are making the mean higher. [The Loudest Number](quest-01-descriptive-statistics.md) showed that the median is then a better typical value than the mean.
* A nested loop runs its inner body once for every outer pass. In Module 1's [Trace the Path](../module-01/quest-01-control-flow.md), 3 worlds × 4 checkpoints printed 12 lines, and grouping by two columns gives every combination the same way.

## Introduction

Sometimes one average hides important differences. For example, two drivers each make 5 deliveries. Sam's deliveries take 40 minutes on average, and Alex's take 25 minutes. Sam's average looks slower than Alex's, but is this true? They each drove different **routes**, the paths a driver follows. A long route outside the city takes 45 minutes, and a trip downtown (in the center of the city) takes 20 minutes.

* Sam drove 4 long routes and 1 downtown trip.
* Alex drove 1 long route and 4 downtown trips.

As in [The Loudest Number](quest-01-descriptive-statistics.md), an average is the sum of the values ÷ the number of values:

* Sam's average = (4 × 45 + 20) ÷ 5 = 200 ÷ 5 = **40 minutes**
* Alex's average = (45 + 4 × 20) ÷ 5 = 125 ÷ 5 = **25 minutes**

On the same route, they are equally fast: both take 45 minutes on a long route and 20 minutes downtown. Sam's average is higher only because Sam drove more long routes. In the picture below, look at Sam's 4 red long routes on the left.

![Two drivers' deliveries. Left, all deliveries: Sam made 4 long-route deliveries, in red, at 45 minutes each, and 1 downtown delivery, in grey, at 20 minutes. Alex made 1 long-route delivery at 45 minutes and 4 downtown deliveries at 20 minutes. Sam's average = (4 × 45 + 20) ÷ 5 = 200 ÷ 5 = 40 minutes. Alex's average = (45 + 4 × 20) ÷ 5 = 125 ÷ 5 = 25 minutes. Sam looks 15 minutes slower because Sam drove 4 long routes. Right, the same route: on the long route both take 45 minutes, and downtown both take 20 minutes, so on the same route they are equally fast.](images/driver-route-mix.svg)

**Main takeaway:** A gap between two averages can come from a **confound** instead of a real difference. A confound is another variable that affects the result, but that you didn't consider at first. Here, the confound is the type of route: Sam looks slow only because Sam drove more long routes. Before you compare the two drivers, count how many long routes and downtown trips each one drove. Then compare them on the same type of route: long vs. long, and downtown vs. downtown.

In the data, each driver's 5 deliveries form a **group**: rows that share the same value, here the same driver. So the same check works for any groups you compare, like two stores or two teams.

**Why it matters at work:** Splitting a number into groups shows what really causes it, before anyone acts on it. For example, teams use it to:

* decide which store, team, or worker needs help
* set fair goals for drivers who work different routes
* plan how many workers each kind of job needs

If you act on a gap that the mix created, you pay for the wrong fix. For example, you might retrain a team that was never slow.

## Learning goals

After this reading, you should be able to say:

* I can split a number by two columns at once to compare every combination.
* Before I compare groups, I can count each type of row in each group (like each driver's long and downtown routes), and spot a confound.
* I can tell a finding worth reporting from one that comes from a tiny group (like Sam's 1 downtown trip) or that everyone already knows.

**Skills:** Data Mining · Statistical Analysis

## Words to know

### Splitting a number into groups

The examples use the 10 deliveries from the Introduction. Each delivery is one row. Its columns are the driver, the route, and the minutes it took.

* Sam: `long 45, long 45, long 45, long 45, downtown 20`
* Alex: `long 45, downtown 20, downtown 20, downtown 20, downtown 20`

| Word | What it means | Example with the 10 deliveries |
| --- | --- | --- |
| **Segment** | Split a number by one or two columns, so each group gets its own value. Splitting by two columns gives every combination. | Minutes split by driver and route: 2 drivers × 2 routes = **4 groups** |
| **Mix** | How many of each type of row a group has. A group's mix can change its average. | Sam: **4 long routes and 1 downtown trip** |
| **`groupby(["driver", "route"])`** | Groups by two columns at once. Pass a list of columns, and you get one group for each combination. | "Sam, long" or "Alex, downtown" |

Each group's label is a pair of values, like `("Sam", "long")`. That's a **tuple**, from [Pick the Right Container](../module-01/quest-04-data-structures.md). A tuple is like a list that can't change:

* A list, `["Sam", "long"]`, can change: `.append("rainy")` adds a third value.
* A tuple, `("Sam", "long")`, can't change. `.append()` gives an error.

Because a tuple can't change, it can be a dictionary key. Here, it works as each group's key.

### Numbers that describe each group

**Units** are what a number counts or measures. In this table, `.size()`, sample size, and count are in rows (here, deliveries). Every other number is in minutes, the same units as the data.

In the Introduction, every long route took exactly 45 minutes, so there is no spread to measure. To show spread, the std and `.agg` rows below add new numbers. Say Sam's 4 long routes next week take 43, 47, 44, and 46 minutes.

| Word | What it means | Example with the deliveries |
| --- | --- | --- |
| **`.size()`** | Counts the rows in each group. | Sam, long = **4 deliveries** |
| **Sample size** | How many rows were used to work out a number. In a tiny group, one unusual row can move the average a lot. | Sam made only **1 downtown delivery**, too few to trust. |
| **Standard deviation (std)** | How far values usually sit from the mean. A small std means the values are close together. | This week's 4 long routes are all 45 minutes: std = **0 minutes**. Next week's 43, 47, 44, and 46 sit close together: std = **1.8 minutes** |
| **`.agg(["count", "mean", "median", "std"])`** | Works out several summaries for each group at once, one column each. `"std"` adds the standard deviation. | For next week's long routes: count **4 deliveries**, mean (43 + 47 + 44 + 46) ÷ 4 = 180 ÷ 4 = **45 minutes**, median (44 + 46) ÷ 2 = **45 minutes**, std **1.8 minutes** |

You've seen a small test mislead before. In [When the Crowd Grows](../module-01/quest-03-big-o-intuition.md), a fast test on a few items didn't prove much. The code could still be slow on many. An average from a tiny group is the same: a few rows can't prove a pattern.

### Is the pattern real?

| Word | What it means | Example with the deliveries |
| --- | --- | --- |
| **Confound** (also called a **confounding variable**) | Another variable that affects the result, but that you didn't consider at first. It can make a gap between groups look real when it isn't. | The type of route, long or downtown. It makes Sam's average 15 minutes higher, even though Sam drives as fast as Alex. |
| **Non-obvious pattern** | A real, checkable finding that the reader wouldn't have guessed from the obvious groups alone, and that they would act on. | The manager gave Sam **4 of the 5 long routes**. That route plan explains the whole gap. |
| **Simpson's paradox** | When a group looks better or worse overall, but the gap shrinks or flips once you compare the same kind of row. The mix causes it. The reading's optional video shows another example. | Overall, Sam takes 40 − 25 = **15 minutes** longer. On the same route, the gap shrinks to **0 minutes**: 45 vs. 45 on long routes, and 20 vs. 20 downtown. |

{% hint style="info" %}
**Ask what else is different about the group.** Before you blame a driver, a team, or a shop for a gap, count each type of row in each group, like each driver's long and downtown routes. Naming what else differs between groups is the habit that catches a confound.
{% endhint %}

## Before you read

In the reading, you'll focus on FixIt, a phone repair shop with two locations. Downtown repairs take about 15 minutes longer on average than Eastside repairs, and the owner asks, "Is Downtown slow?"

Think about: what would you want to know before you answer? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

As you read, look for:

1. What happens to the 15-minute gap when you compare the same repair type at both shops.
2. Why one of the group averages is too small to trust.
3. What makes the old-phone finding worth telling the owner, when "screen repairs take longer" isn't.

**[Start the reading: Beneath the Total →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/mining-a-pattern/reading-1-beneath-the-total/)** (about 20 minutes)

## Main takeaways

### Summary

* **Count the mix before you compare groups.** When one group looks much better or worse, run `groupby([...]).size()` to count each type of row in each group, like each driver's long and downtown routes. Then compare the groups on the same type of row, like long route vs. long route.
* **A finding worth reporting** is real, checkable, and something the reader would act on. It holds in every group and comes from enough rows. "Long routes take longer than downtown trips" is true, but the manager already knows it.
* **Use the statistic that fits.** The mean is fine when it's close to the median and the std is small. For Sam's long routes next week, the mean and the median are both 45 minutes, and the std is 1.8 minutes. So the mean is fine.

In the reading, FixIt's two shops show the same kind of gap. The picture below follows the reading's FixIt repairs. On the left, look at the 15-minute gap. On the right, look at the same two shops with screen repairs only.

![Two bar charts of FixIt's repair times, with a y-axis of average minutes. Left, all repairs: Downtown 45.7 minutes and Eastside 30.5, about 15 minutes apart. Right, screen repairs only: Downtown 50.0 and Eastside 51.0, about the same. Downtown did 5 screen repairs and 1 battery repair. Eastside did 2 and 4. Screen repairs take longer.](images/confound-gap.svg)

In the reading, the gap came from the mix, just like Sam's: Downtown did more screen repairs, which take longer. Back to the drivers: Sam made only 1 downtown trip, and Alex made only 1 long route. Because those counts are small, the next step is to check the pattern over more weeks.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Sam's average is 15 minutes higher, so Sam is slow." | Sam drove 4 long routes and 1 downtown trip. Alex drove 1 and 4. Both take 45 minutes on a long route and 20 minutes downtown. The type of route is a confound. |
| "I'll always report the median, just to be safe." | Pick the one that fits. For Sam's long routes next week, the mean and the median are both 45 minutes. The std is 1.8 minutes. So the mean is fine. |
| "It's true, so it's a finding." | "Long routes take longer than downtown trips" is true, but the manager already knows it. "Sam got 4 of the 5 long routes, and that explains the gap" is new to the manager, so it's a finding. |

### How this connects

* **Next reading:** You'll take a pattern like this and question the data behind it: who collected it, what's missing, and which groups got counted less. Then you'll write questions specific enough that the person who looks after the data could answer them.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll look for a non-obvious finding in a real dataset. Before you report a gap between groups, you'll check each group's mix and size, and compare the same kind of row across groups.

## Quick check

**1.** Next month, Alex's average delivery time is 12 minutes higher than Sam's. The manager wants to retrain Alex. What do you check first?

<details>
<summary>Answer</summary>

The mix. Run `groupby(["driver", "route"]).size()` to see whether Alex drove more long routes. Then compare the same route across drivers.

</details>

**2.** Next month, Sam's 1 downtown trip takes 30 minutes. A coworker says, "Sam is slower downtown than Alex." Report it?

<details>
<summary>Answer</summary>

Not yet. One delivery is too few to trust. Check it with more data first.

</details>

---

**Next:** [Quest 2.9 — The Pattern Isn't the Proof: Asking Questions About Your Data (Day 10)](quest-09-clarifying-questions.md)
