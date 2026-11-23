# Quest 2.5 — Real Numbers, Wrong Story: Chart Best Practices (Day 5)

**Total time:** about 30 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Sometimes a chart tells a story that its numbers don't support. For example, an ad (an advertisement) shows two bars for phone battery life: 20 hours for one phone and 19 hours for another. The y-axis starts at 18, so the first bar looks twice as tall. But the real difference is only about 5%.

![Two bar charts of the same data: phone A lasts 20 hours and phone B lasts 19 hours. Left chart: the y-axis starts at 18, so phone A's bar looks twice as tall as phone B's. Right chart: the y-axis starts at 0, so the bars look almost the same height, which matches the real difference of about 5%.](images/axis-baseline.svg)

In this reading, you'll learn:

* two ways a chart with real numbers can still mislead:
  * a y-axis that doesn't start at zero
  * hidden outliers
* the labels every shared chart needs

**Main takeaway:** Every number can be correct and the chart can still tell the wrong story. Before you share a chart, check where the axis starts and what the chart leaves out.

**Why it matters at work:** People make decisions based on how a chart looks, often without seeing your code. A misleading chart can send money, staff, or time to the wrong place.

## Learning goals

Check off each goal once you can do it.

- [ ] I can spot a bar chart whose y-axis doesn't start at zero, and fix it.
- [ ] I can tell when a boxplot is hiding outliers, and say so in a caption.
- [ ] I can label a chart so any reader can follow it: a title that states the finding, axes with units, a legend, and colors that work for colorblind readers.

**Skills:** Data Visualization · Data Distributions & Shape · Critical Thinking

## Quick recall

You've learned to label a chart, and to doubt a result that only looks right. This reading puts the two together.

* Recall that to compare one number across groups, like an average for each group, you pick a bar chart. You also gave a polished chart a title that states the finding and axis labels with units, using `plt.title("...")` and `plt.ylabel("...")`, in [Who's This Chart For?](quest-04-two-kinds-of-charts.md).
* Recall that Q1 is the value a quarter of the sorted data falls below, and Q3 is the value three quarters falls below. You found them in the five-number summary in [The Loudest Number](quest-01-descriptive-statistics.md). Here you'll use them to find where outliers start.
* Recall that code can run with no error and still print a wrong answer, from [Looks Right. Is It?](../module-01/quest-10-debugging.md). So you worked out the expected answer by hand first, then compared.

## Words to know

### Reading a chart's axes

| Word | What it means |
| --- | --- |
| **Axis** | One of the two lines along the edge of a chart. The **x-axis** runs across the bottom. The **y-axis** runs up the side. |
| **Scale** | The numbers marked along an axis, from the lowest to the highest. |
| **Baseline** | Where the bars start. On an honest bar chart, the baseline is zero. |
| **Truncated axis** | A y-axis that doesn't start at zero. On a bar chart, it makes small real differences look big. |
| **Slope** | How steeply a line goes up or down from one point to the next. A line chart's claim (what the chart says is true) is its slope, not its height. |

Use your expected-answer habit on charts, too. 191 swimmers is only about 5% more than 182. So if one bar looks five times taller than the other, the chart is wrong, not the numbers.

### Outliers and boxplots

| Word | What it means | Units |
| --- | --- | --- |
| **Outlier** | A value far from the rest. It can still be real. | Same as the data (here, laps: one lap is one swim from one end of the pool to the other) |
| **Boxplot** | A chart of one column's spread: a box from Q1 to Q3, a line at the median, and whiskers above and below. Outliers show as dots. | Same as the data |
| **Whisker** | The line that sticks out of the box. The top whisker stops at the largest value inside the upper fence. | Same as the data |
| **Box height** | Q3 − Q1: how tall the box is. (This is the IQR.) | Same as the data |
| **Upper fence** | The outlier cutoff: Q3 + 1.5 × (Q3 − Q1). Points past it are outliers. | Same as the data |

### Labels that travel with a chart

| Word | What it means |
| --- | --- |
| **Data series** | One set of values drawn on a chart, like one line or one set of bars. (This is a charting word. It isn't the same as a pandas Series, which is one column of a table.) |
| **Legend** | A small key that says which color or pattern is which data series. Needed when a chart has more than one data series. |
| **Caption** | A short note under a chart, like "1 swim of 110 laps is not shown." |
| **Chart junk** | Decoration that doesn't help a reader, like 3D effects or extra gridlines. |
| **Colorblind-safe palette** | Colors that differ in lightness, not just in hue, so readers who can't tell red from green can still tell them apart. |

### Code in this reading

| Code | What it does |
| --- | --- |
| **`.plot.bar(rot=0)`** | Draws one bar per group. The parameter `rot` is set to `0`, which keeps the group labels flat (rotated 0 degrees). |
| **`plt.ylim(180, 195)`** | Sets the y-axis to run from 180 to 195. On a bar chart, this cuts off the baseline. |
| **`.quantile([0.25, 0.75])`** | Gives Q1 and Q3 of a column. |
| **`.max()`** | Gives the largest value in a column. |
| **`.plot.box()`** | Draws a boxplot. |
| **`showfliers`** | A parameter of the boxplot method. Setting `showfliers` to `False` leaves every outlier dot out of the drawing. The default is `True`. |

`showfliers=False` is risky for the same reason a bare `except:` is, from [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md). Both hide something without any warning, and the result still looks fine.

## Before you read

In the reading, you'll focus on a city's three public pools. The pool manager is making a chart for the city council, which decides where to send more lifeguards. The **city council** is the group of elected leaders who make decisions for the city. **Lifeguards** are workers who watch swimmers and keep them safe. The pools average 182, 188, and 191 swimmers a day, but the draft chart makes the busiest pool look about five times busier than the quietest.

Think about: how can a chart make a gap that big when every number in it is real? Write down your first answer, then see if the reading agrees.

## Read

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
| "Real numbers can't tell a wrong story." | The axis and the settings can. Check the picture, not just the data. |
| "Every chart's y-axis has to start at zero." | Bar charts do. A labeled line chart can zoom in to show change. |
| "New colors fix a misleading chart." | Colors don't change the axis. Delete the line that cuts it off. |
| "Delete the outlier's row so the data matches the tidy chart." | A real value stays in the data. Show it, or hide it only with a caption that says what's missing. |

### How this connects

* **Next:** A practice day with no new reading. You'll review what you've learned so far, and practice checking analysis code that an AI (artificial intelligence) tool writes for you. Later, you'll run these same two chart checks when an AI writes or describes a chart for you.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Every chart you share will need to fit its question and be labeled honestly: a y-axis that starts where it should, nothing hidden without a note, and a title and axes a reader can follow without your code.

## Quick check

**1.** A boxplot's top whisker stops at 34 laps. The column's `.max()` is 110. What happened?

<details>
<summary>Answer</summary>

The boxplot was drawn with `showfliers=False`, which hid the 110-lap outlier. Show it, or add a caption saying it's hidden.

</details>

**2.** A line chart of weekly swimmers zooms the y-axis to 900–1,000. Is that honest?

<details>
<summary>Answer</summary>

Yes, as long as the axis is labeled. A line chart's claim is the change from week to week, so zooming in is fine. A bar chart would need to start at zero.

</details>

---

**Next:** [Practice Day: Review (Day 6)](practice-day-06.md)
