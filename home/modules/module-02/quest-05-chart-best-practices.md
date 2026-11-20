# Quest 2.5 — Real Numbers, Wrong Story (Day 5)

{% hint style="info" %}
**In one sentence:** A chart can use only real numbers and still mislead, so check where the axis starts and what the chart leaves out before you share it.
{% endhint %}

## Why this matters

People decide things from how a chart looks, often without seeing your code. A city council might send lifeguards to the wrong pool because one bar looked five times taller than it should. Catching that is part of your job.

## What you'll be able to do

* I can spot a cut-off y-axis on a bar chart and fix it.
* I can find outliers a boxplot is hiding and say so in a caption.
* I can label a chart so it makes sense for any reader, including people who are colorblind.

**Skills:** Data Visualization · Data Distributions & Shape · Critical Thinking

## Words to know

| Word | What it means |
| --- | --- |
| **Truncated axis** | A y-axis that doesn't start at zero. On a bar chart, it makes small differences look big. |
| **Boxplot** | A chart of one column's spread: a box from Q1 to Q3, a line at the median, and whiskers. |
| **Upper fence** | The outlier cutoff: Q3 + 1.5 × (Q3 − Q1). Points past it are outliers. |
| **`showfliers`** | A boxplot setting. `showfliers=False` hides every outlier dot. |
| **Chart junk** | Decoration that doesn't help a reader, like 3D effects or extra gridlines. |
| **Colorblind-safe palette** | Colors that differ in lightness, so readers who can't tell red from green can still tell them apart. |

## Before you read

Three pools average 182, 188, and 191 swimmers a day. A bar chart makes the busiest pool look five times busier than the quietest. Can every number be real and the chart still be wrong?

<details>
<summary>Answer</summary>

Yes. If the y-axis starts at 180 instead of 0, the bars show only the part above 180, so a 5% gap looks huge.

</details>

## Read

**[Start the reading: Real Numbers, Wrong Story →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/chart-best-practices/reading-1-onechartonepoint/)** (about 19 minutes)

As you read, look for:

1. The one line of code that made the pool chart mislead.
2. How to tell that a boxplot looks "too tidy."
3. The five labeling habits that travel with a chart into slides and emails.

## Main takeaways

### Summary

* **A bar's height is the claim, so a bar chart's y-axis starts at zero.** Look for any `plt.ylim(...)` line. A line chart can zoom in, because its claim is the change from point to point, not the height.
* **`showfliers=False` hides outliers.** Compare the top of the chart with the column's real `.max()`. If you hide anything, say so in a caption.
* **Label everything:** a title that states the finding, both axes with units, a legend when there's more than one series, no chart junk, and colors that don't rely on red vs. green.

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

### How this connects

* **Next:** Day 6 is a practice day. Then Quest 2.10 uses these same checks on charts an AI describes or suggests.
* **Boss Battle:** Your charts are graded on fitting the question and being labeled honestly. The Above & Beyond item asks you to show a first draft and a fixed version side by side.

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

**Next:** [Practice Day — Stats, pandas, Charts](practice-day-06.md)
