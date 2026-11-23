# Quest 2.4 — Who's This Chart For? Exploratory vs. Explanatory Charts (Day 4)

**Total time:** about 30 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Introduction

Sometimes the same numbers need two different charts. For example, a coffee shop owner draws a quick chart of daily sales to find her slow days. Later, she asks a bank for a loan. The chart for the bank needs a clear title, labeled axes, and nothing extra, because the banker never saw her first chart.

In this reading, you'll learn how to:

* tell a chart made for you apart from a chart made for someone else
* choose a chart type on purpose
* chart a count over time

**Main takeaway:** Before you make a chart, ask two questions: Who is this chart for? What am I comparing? Also check a number before you trust a picture.

**Why it matters at work:** People will judge every chart you share, and most of them never saw your notebook. If the chart type doesn't fit the question, or the title doesn't say what you found, the reader may miss your point.

## Learning goals

Check off each goal once you can do it.

- [ ] I can tell an exploratory chart (for me) apart from an explanatory chart (for a stakeholder), and make the three changes that turn one into the other.
- [ ] I can choose a chart type by asking what I'm comparing.
- [ ] I can turn a text column into real dates and chart a count over time.

**Skills:** Data Visualization · Stakeholder Communication

## Quick recall

* Recall that a group summary gives you one row per group, from [One Row Per Group](quest-03-group-columns.md): `drives.groupby("site")["units"].mean()` gives one average per site.
* Recall that double brackets pick a list of columns, from [Look Before You Filter](quest-02-inspect-filter.md): `df[["category", "weight_lbs"]]` keeps just those two columns.

## New tool: Matplotlib

**What it's for:** Matplotlib is a free Python package for drawing charts. In this reading, pandas draws the chart with `.plot`, and Matplotlib (`plt`) adds the title and axis labels and shows the chart under the cell.

**How you'll see it in this reading:**

```python
import matplotlib.pyplot as plt  # load the chart module

students.plot.scatter(x="hours", y="score_gain", alpha=0.6)
plt.title("More tutoring hours went with slightly bigger gains")
plt.ylabel("Reading score gain (points)")
plt.show()

daily.plot(rot=45)
```

**Code walkthrough:**

1. `matplotlib.pyplot` is the **module** inside the Matplotlib package that draws charts. This line loads it and gives it the short name `plt`.
2. `students.plot.scatter(...)` is a pandas **method** that draws a scatterplot, with one dot per row. This line sets three parameters. The parameter `x` is set to `"hours"`, the column for the x-axis (across the bottom). The parameter `y` is set to `"score_gain"`, the column for the y-axis (up the side). The parameter `alpha` is set to `0.6`, which makes the dots a bit see-through (0 is invisible and 1 is solid), so overlapping dots are easier to see.
3. `plt.title(...)` and `plt.ylabel(...)` are **functions** from the `plt` module. They put a title over the chart and label the y-axis.
4. `plt.show()` draws the finished chart under the cell.
5. `daily.plot(rot=45)` draws a line chart. The parameter `rot` is set to `45`, which rotates (turns) the x-axis labels 45 degrees so long dates don't overlap.

The x-axis, across the bottom, has its own label function with a matching name. The reading asks you to find it. If `import matplotlib` gives a `ModuleNotFoundError` on your laptop, run `pip install matplotlib` in the terminal once.

**Learn more:** [Matplotlib: Quick start guide](https://matplotlib.org/stable/users/explain/quick_start.html) (official) · [pandas: Chart visualization](https://pandas.pydata.org/docs/user_guide/visualization.html) (official, every `.plot` chart type with pictures) · [W3Schools: Matplotlib Pyplot](https://www.w3schools.com/python/matplotlib_pyplot.asp)

## Words to know

### Two kinds of charts

| Word | What it means |
| --- | --- |
| **Exploratory chart** | A quick, rough chart you make for yourself to find a pattern. No title, raw column names as labels. That's fine, because nobody else sees it. |
| **Explanatory chart** | A polished chart, chosen on purpose, that tells a stakeholder one clear finding. Every explanatory chart starts as a rough one. |
| **Stakeholder** | The person a finding is for, who wasn't there while you explored. In the reading, the grant committee. |
| **Finding title** | A chart title that states what you found, in under 10 words, like "Sign-ins jumped the day before the test." A title that only names the columns makes the reader work out the point alone. |

### Parts of a chart

| Word | What it means |
| --- | --- |
| **x-axis** | The line across the bottom of a chart. |
| **y-axis** | The line up the side of a chart. |
| **Axis label** | The words on an axis that say what it measures, in plain words, with units: "Tutoring time (hours)," not `hours`. |

### Chart types

| Word | What it means | Use it when you're comparing... |
| --- | --- | --- |
| **Histogram** | Bars that count how many values fall in each range. | One column's shape |
| **Boxplot** | A box that shows the middle half of the values, with a line at the median and lines out to the low and high values. It's the five-number summary as a picture. | One column's shape, or the spread inside each group |
| **Line chart** | Points joined in order, to show change from one time to the next. | A change over time |
| **Scatterplot** | One dot per row, with one number column across and another up the side. | Two number columns |
| **Bar chart** | One bar per group, with the bar's height showing a number. | One number across groups |

### The numbers behind the charts

| Word | What it means | Units |
| --- | --- | --- |
| **Correlation** | A number for how closely two number columns move together. Near 1 means one goes up when the other does, almost every time. Near 0 means a weak link. `.corr()` works it out for every pair of columns you give it. | No units. Always between -1 and 1 |
| **Datetime** | A pandas column type that stores real dates and times, so you can pull out the day, month, or weekday. `pd.to_datetime(...)` turns text like `"2026-03-02 15:30"` into a datetime. | — |
| **`.dt.date`** | Keeps just the calendar day of each date and time, so you can group rows by day. | — |
| **`.size()`** | After a groupby, counts the rows in each group. | A count of rows (in the reading, sign-ins per day) |
| **Series** | A single pandas column of values with labels, like the counts per day. A Series's `.plot()` draws a line chart unless you ask for another kind. | — |

## Before you read

In the reading, you'll focus on a free after-school tutoring center that's asking a city grant committee for money. The director asks you for one chart that shows how tutoring helps.

Think about: what should be different between the charts you make while exploring the data and the one chart you hand the committee? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. The three changes that turn a rough chart into a chart for someone else.
2. Why you check `.corr()` before you trust a chart, or an AI's words about it.
3. The steps that turn sign-in times into a count of sign-ins per day.

**[Start the reading: Who's This Chart For? →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/exploratory-vs-explanatory-charts/reading-1-whoschartisfor/)** (about 20 minutes)

## Main takeaways

### Summary

* **Exploratory charts are for you:** fast and rough. **Explanatory charts are for a stakeholder:** one finding, a title that states it in under 10 words, axis labels in plain words with units, and nothing extra.
* **Check a number before you trust a picture.** A correlation of 0.26 is weak, so write "tended to," not "strong," even if an AI's description of the chart sounds sure.
* **Pick the chart by what you're comparing.** To chart a count over time: `pd.to_datetime`, group by `.dt.date`, `.size()`, then `.plot()` for a line.

![Four cards under the question "Pick a chart by asking: what am I comparing?" One column's shape: histogram or boxplot, for example how gifts are spread out. A change over time: line chart, for example sign-ins per day. Two number columns: scatterplot, for example hours vs. score gain. One number across groups: bar chart, for example average swimmers per pool, with the y-axis starting at zero.](images/chart-chooser.svg)

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "A good title names the columns." | A good title states the finding. Column names belong on the axes, in plain words with units. |
| "A weak correlation means the chart failed." | A weak link is still a finding. Describe it honestly. |
| "Grades 6, 7, and 8 are in order, so use a line chart." | You're comparing groups, so use a bar chart. Lines are for change over time. |
| "One busy week shows a trend." | One week can show a spike. A long-term trend needs months of data. |

### How this connects

* **Next reading:** You'll check these same chart types for honesty: where an axis starts, and what a chart leaves out.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** When you share findings, you'll choose a chart type for each question, say why you chose it, and polish the charts you share so a reader who never saw your notebook gets the point.

## Quick check

**1.** The director wants to know whether students who read more books at home gain more points. Which chart fits?

<details>
<summary>Answer</summary>

A scatterplot. You're comparing two number columns: books read and points gained.

</details>

**2.** You paste a rough chart into an AI chat. It says, "There's a strong relationship." Your `.corr()` shows 0.26. What do you write?

<details>
<summary>Answer</summary>

That the two tended to rise together, but the link is weak. Your number settles the claim, not the AI's wording.

</details>

---

**Next:** [Quest 2.5 — Real Numbers, Wrong Story: Chart Best Practices (Day 5)](quest-05-chart-best-practices.md)
