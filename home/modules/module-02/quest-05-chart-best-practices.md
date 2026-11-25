# Quest 2.5 — Real Numbers, Wrong Story: Chart Best Practices (Day 5)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Quick recall

You've learned to label a chart, and to doubt a result that only looks right. This reading puts the two together.

* A bar chart compares one number across groups, like an average for each group. In [Who's This Chart For?](quest-04-two-kinds-of-charts.md), you also gave a polished chart a finding title and axis labels with units, using `plt.title("...")` and `plt.ylabel("...")`.
* Q1 and Q3 come from the five-number summary in [The Loudest Number](quest-01-descriptive-statistics.md): a quarter of the sorted data falls below Q1, and three quarters below Q3. Here you'll use them to find where outliers start.
* Code can run with no error and still print a wrong answer, as in Module 1's [Looks Right. Is It?](../module-01/quest-10-debugging.md). So you worked out the expected answer by hand first, then compared.

## Introduction

Sometimes a chart tells a story that its numbers don't support. For example, an ad (an advertisement) shows two bars for phone battery life. Phone A lasts 20 hours, and phone B lasts 19 hours. The y-axis starts at 18, so each bar shows only the part above 18:

* Phone A's bar: 20 − 18 = 2 hours tall
* Phone B's bar: 19 − 18 = 1 hour tall

So phone A's bar looks twice as tall. But phone A lasts only 1 hour longer. To turn that into a percent, divide the difference by phone B's hours, then multiply by 100:

* Percent longer = (20 − 19) ÷ 19 × 100 = 1 ÷ 19 × 100 = about **5%**

Now compare the two charts in the picture below. Only the start of the y-axis changes.

![Two bar charts of the same data: phone A lasts 20 hours and phone B lasts 19 hours. Left chart: the y-axis starts at 18, so phone A's bar looks twice as tall as phone B's. Right chart: the y-axis starts at 0, so the bars look almost the same height, which matches the real difference of about 5%.](images/axis-baseline.svg)

**Main takeaway:** A chart can mislead even when every number in it is right. One common cause is a **truncated axis**: a y-axis that doesn't start at zero. The battery chart's y-axis starts at 18. Before you share a chart, check where the y-axis starts and what the chart leaves out.

**Why it matters at work:** People make decisions based on how a chart looks, often without seeing your numbers or code. For example, leaders use charts to decide:

* which location gets more staff
* where to spend next year's budget (a plan for how much money to spend)
* which product to stop selling

A chart can make a 5% gap look like twice as much. Then money, staff, or time can go to the wrong place.

## Learning goals

After this reading, you should be able to say:

* I can spot a bar chart whose y-axis doesn't start at zero, and fix it.
* I can tell when a boxplot is hiding outliers, and say so in a caption.
* I can label a chart so any reader can follow it: a title that states the finding, axes with units, a legend, and colors that work for colorblind readers.

**Skills:** Data Visualization · Data Distributions & Shape · Critical Thinking

## Words to know

### Reading a chart's axes

The examples use the phone battery charts from the Introduction.

| Word | What it means | Example |
| --- | --- | --- |
| **Axis** | One of the two lines along the edge of a chart. The **x-axis** runs across the bottom. The **y-axis** runs up the side. | The x-axis names the 2 phones. The y-axis shows battery life in hours. |
| **Scale** | The numbers marked along an axis, from the lowest to the highest. | 18 to 20 hours in the left phone chart |
| **Baseline** | Where the bars start. On a bar chart, the baseline should be zero. | 18 in the left phone chart, 0 in the right one |
| **Truncated axis** | A y-axis that doesn't start at zero. On a bar chart, it makes small real differences look big. | The left phone chart's y-axis, which starts at 18 |
| **Slope** | How steeply a line goes up or down from one point to the next. A line chart's claim (what the chart says is true) is its slope, not its height. | In the last reading's sign-ins chart, the line jumps from 1 on March 5 to 5 on March 6. That's a steep slope. |

The reading's pool chart has the same problem. Use your expected-answer habit, and work out the real gap first:

* (191 − 182) ÷ 182 × 100 = 9 ÷ 182 × 100 = about **5%** more swimmers

Now look at the draft chart, where the y-axis starts at 180. Riverside's bar shows 191 − 180 = 11. Eastside's bar shows 182 − 180 = 2. So Riverside's bar looks 11 ÷ 2 = 5.5 times taller. When the picture and the numbers disagree that much, the chart is wrong, not the numbers.

### Outliers and boxplots

**Units** are what a number counts or measures. Every number in this table is in laps, the same units as the data. One **lap** is one swim from one end of the pool to the other. The examples use the 10 swims from the reading, sorted:

`12, 18, 20, 22, 24, 25, 28, 30, 34, 110` (in laps)

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Outlier** | A value far from the rest. It can still be real. | Jae's swim of **110 laps**. The other 9 are 12 to 34 laps. |
| **Boxplot** | A chart of one column's spread: a box from Q1 to Q3, a line at the median, and whiskers above and below. Outliers show as dots. | Box from Q1 = **20.5** to Q3 = **29.5**, with a line at the median, **24.5 laps** |
| **Whisker** | The line that sticks out of the box. The top whisker stops at the largest value inside the upper fence. | The top whisker stops at **34 laps** |
| **Box height** | Q3 − Q1: how tall the box is. (This is the IQR.) | 29.5 − 20.5 = **9 laps** |
| **Upper fence** | The outlier cutoff: Q3 + 1.5 × (Q3 − Q1). Points past it are outliers. | 29.5 + 1.5 × 9 = 29.5 + 13.5 = **43 laps**. 110 is past it. |

### Labels that travel with a chart

| Word | What it means | Example in the reading |
| --- | --- | --- |
| **Data series** | One set of values drawn on a chart, like one line or one set of bars. (This is a charting word. It isn't the same as a pandas Series, which is one column of a table.) | The 3 bars of average swimmers are one data series |
| **Legend** | A small key that says which color or pattern is which data series. Needed when a chart has more than one data series. | Needed if each pool had a Monday bar and a Tuesday bar |
| **Caption** | A short note under a chart. | "1 swim of 110 laps is not shown." |
| **Chart junk** | Decoration that doesn't help a reader, like 3D effects or extra gridlines. | 3D bars on the pool chart |
| **Colorblind-safe palette** | Colors that differ in lightness, not just in hue (color name), so readers who can't tell red from green can still tell them apart. | Not a red Eastside bar next to a green Riverside bar. About 1 in 12 men can't easily tell them apart. |

### Code in this reading

| Code | What it does |
| --- | --- |
| **`.plot.bar(rot=0)`** | Draws one bar per group. The parameter `rot` is set to `0`, which keeps the group labels flat (rotated 0 degrees). |
| **`plt.ylim(180, 195)`** | Sets the y-axis to run from 180 to 195. On a bar chart, this cuts off the baseline. |
| **`.quantile([0.25, 0.75])`** | Gives Q1 and Q3 of a column. For the laps: **20.5** and **29.5**. |
| **`.max()`** | Gives the largest value in a column. For the laps: **110**. |
| **`.plot.box()`** | Draws a boxplot. For the laps, the box runs from **20.5** to **29.5**, and **110** shows as a dot. |
| **`showfliers`** | A parameter of the boxplot method. Setting `showfliers` to `False` leaves every outlier dot out of the drawing. The default is `True`. |

`showfliers=False` is risky for the same reason a bare `except:` is, from [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md). Both hide something without any warning, and the result still looks fine.

## Before you read

In the reading, you'll focus on a city's three public pools. The pool manager is making a chart for the city council, which decides where to send more lifeguards. The **city council** is the group of elected leaders who make decisions for the city. **Lifeguards** are workers who watch swimmers and keep them safe. The pools average 182, 188, and 191 swimmers a day, but the draft chart makes the busiest pool look about five times busier than the quietest.

Think about: how can a chart make a gap that big when every number in it is real? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

As you read, look for:

1. The one line of code that made the pool chart mislead, and what happens when you delete it.
2. How to tell that a boxplot looks "too tidy."
3. The five labeling habits that travel with a chart into slides and emails.

**[Start the reading: Real Numbers, Wrong Story →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/chart-best-practices/reading-1-onechartonepoint/)** (about 19 minutes)

## Main takeaways

### Summary

* **A bar's height is the claim, so a bar chart's y-axis starts at zero.** pandas starts bars at zero on its own, so look for any line that sets axis limits, like `plt.ylim(...)`. A line chart can zoom in, because its claim is the slope, the change from point to point.
* **`showfliers=False` hides outliers.** Compare the top of the chart with the column's real `.max()`. If you hide anything, say so in a caption.
* **Label everything:** a title that states the finding, both axes with units, a legend when there's more than one data series, no chart junk, and colors that don't rely on red vs. green.

| Before you share a chart, ask | How to check |
| --- | --- |
| Where does the y-axis start? | Look for `plt.ylim`. Bar charts start at zero. |
| Was anything left out of view? | Compare the chart's top with `.max()`, and look for `showfliers=False`. |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "Every number in my chart is right, so the chart can't mislead." | The axis can. With the y-axis starting at 18, phone A's 5% lead looks like twice as much. Check the picture, not just the data. |
| "Every chart's y-axis has to start at zero." | Bar charts do. A labeled line chart of weekly swimmers can run from 900 to 1,000 to show the change. |
| "If I change the colors, the chart won't mislead anymore." | Colors don't change the axis. Delete the `plt.ylim(180, 195)` line that cuts it off. |
| "I'll delete Jae's 110-lap row so the data matches the tidy chart." | Jae's swim is real, so it stays in the data. Show it, or hide it only with a caption: "1 swim of 110 laps is not shown." |

### How this connects

* **Next:** A practice day with no new reading. You'll review what you've learned so far, and practice checking analysis code that an AI (artificial intelligence) tool writes for you. Later, you'll run these same two chart checks when an AI writes or describes a chart for you.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Every chart you share will need to fit its question and be labeled so it doesn't mislead: a y-axis that starts where it should, nothing hidden without a note, and a title and axes a reader can follow without your code.

## Quick check

**1.** A boxplot's top whisker stops at 34 laps. The column's `.max()` is 110. What happened?

<details>
<summary>Answer</summary>

The boxplot was drawn with `showfliers=False`, which hid the 110-lap outlier. Show it, or add a caption saying it's hidden.

</details>

**2.** A line chart of weekly swimmers zooms the y-axis to 900–1,000. Is that misleading?

<details>
<summary>Answer</summary>

No, as long as the axis is labeled. A line chart's claim is the change from week to week, so zooming in is fine. A bar chart would need to start at zero.

</details>

---

**Next:** [Practice Day: Review (Day 6)](practice-day-06.md)
