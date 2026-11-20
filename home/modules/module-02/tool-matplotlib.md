# Tool Guide: Matplotlib

{% hint style="info" %}
**In one sentence:** Matplotlib is a free Python library for drawing charts and saving them as image files.
{% endhint %}

## Why analysts use it

A chart shows a pattern faster than a table of numbers. Analysts use charts twice: once to explore data for themselves, and again to explain a finding to someone else. Matplotlib is the charting tool most other Python chart tools are built on, including pandas' own `.plot()`.

## How it works with pandas

You'll usually start a chart from pandas with `.plot`, then use Matplotlib (`plt`) to add a title and labels, and to show or save it.

```python
import matplotlib.pyplot as plt

df["books_brought"].plot.hist(bins=12)        # pandas draws the chart
plt.title("Most customers trade in under 8 books")  # Matplotlib adds the words
plt.xlabel("Books brought")
plt.ylabel("Customers")
plt.savefig("images/tradeins.png", dpi=150)   # save it BEFORE show
plt.show()
```

## What you'll learn about it in Module 2

| Where | What you'll do |
| --- | --- |
| Quest 2.4 (Day 4) | Draw scatterplots and line charts, and add a title and labels |
| Quest 2.5 (Day 5) | Draw bar charts and boxplots, and catch settings that mislead |
| Quest 2.10 (Day 11) | Save a chart as an image to give to an AI |
| Quest 2.11 (Day 12) | Save a chart into an `images` folder for your README |

## Common first-day problems

| Problem | Fix |
| --- | --- |
| The saved image is blank | `plt.savefig(...)` has to come **before** `plt.show()`. Showing a chart clears it. |
| `ModuleNotFoundError: No module named 'matplotlib'` | Run `pip install matplotlib` in your project's environment. |
| Dates overlap on the x-axis | Add `rot=45` inside `.plot(...)` to tilt them. |

You may also see **seaborn** and **plotly**. Both are allowed in this module, but you don't need them. Everything you need here works with pandas and Matplotlib.

## Getting started resources

* [pandas: Chart visualization](https://pandas.pydata.org/docs/user_guide/visualization.html) (official, every `.plot` chart type with pictures)
* [Matplotlib: Quick start guide](https://matplotlib.org/stable/users/explain/quick_start.html) (official)
* [From Data to Viz](https://www.data-to-viz.com/) (a chart picker that starts from what your data looks like)

---

**Next:** [Quest 2.4 — Who's This Chart For?](quest-04-two-kinds-of-charts.md)
