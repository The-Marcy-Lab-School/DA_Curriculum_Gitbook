# Quest 2.1 — The Loudest Number (Descriptive Statistics)

**Day 1** · Total time: about 30 minutes (this page: about 10 minutes + the interactive reading: about 20 minutes)

## Introduction

Sometimes averages can be misleading. For example, on a street of ten homes, nine sell for about $300,000 and one mansion sells for $3 million. The average price is $570,000, but no home on that street sold for anything close to it. This reading covers when to use the average (the mean), when the middle value (the median) works better, and how to describe how spread out a set of numbers is. The main takeaway: averages are widely used and easy to understand, but they don't always tell the whole story, so look at the data's shape before you pick a number.

**Why it matters at work:** "What's typical?" (what's the usual, normal value?) and "How spread out is it?" are two of the most common questions an analyst answers. If you report the wrong number, people plan budgets and goals around something that isn't true.

## Learning goals

Check off each goal once you can do it.

- [ ] I can find the mean, median, and mode, and explain which one describes "typical" for a set of numbers.
- [ ] I can describe how spread out data is with the standard deviation and the five-number summary, and say what units each one is in.
- [ ] I can tell whether data is skewed, and keep a real outlier while reporting it on its own.

**Skills:** Statistical Analysis · Data Distributions & Shape

## Quick recall

* Recall that you added up a week of step counts with a running total (`total += steps`) in [One Job at a Time](../module-01/quest-07-second-function.md). An average goes one step further: divide the total by how many values there are, `sum(steps) / len(steps)`.
* Recall that a **parameter** is a name in a function's `def` line, and an **argument** is the value you pass in when you call it, from [Build It Once, Use It Again](../module-01/quest-02-functions-scope.md). The functions in this reading have parameters too.
* Recall that a list keeps its items in order, and you can read one item by its position, called its **index**. `sorted_gifts[1]` is the *second* item, because Python starts counting positions at 0: `sorted_gifts[0]` is the first item. You'll use this idea to find the middle value of a sorted list.

## New tool: NumPy

**What it's for:** NumPy does math on many numbers at once. Plain Python lists can add and count, but they don't have a median or a standard deviation built in. NumPy does, so each answer takes one line.

NumPy is a Python **package** (some people say *library*): a collection of code other people wrote. Recall that you loaded a **module** that comes with Python by writing `import json`. You load a package the same way, with `import`. The difference: a package is a bigger set of modules, and it doesn't come with Python, so you install it yourself, once.

**How you'll see it in this reading:**

```python
import numpy as np  # load the package

gifts = np.array([50, 40, 65, 50, 75, 45, 60, 50, 70, 55, 5000])

np.mean(gifts).round(2)         # 505.45
np.median(gifts)                # 55.0
np.std(gifts, ddof=1).round(2)  # 1490.71
np.percentile(gifts, [0, 25, 50, 75, 100])
```

**Code walkthrough:**

1. `import numpy as np` loads the NumPy package and gives it the short name `np`.
2. `np.array([...])` turns a list into an **array**, NumPy's version of a list. One math step works on every value inside it.
3. `np.mean(...)` and `np.median(...)` are NumPy **functions** that find the mean and the median. `.round(2)` is a **method**, a function that belongs to the number NumPy gives back. It rounds that number to 2 decimal places.
4. `np.std(gifts, ddof=1)` finds the standard deviation. This line sets the parameter `ddof` to the argument `1`. That tells NumPy to use the **sample** formula, which divides by one less than the number of values. It's the version pandas and most other tools use, so your answers will match theirs.
5. `np.percentile(gifts, [0, 25, 50, 75, 100])` gives the five-number summary in one line. Each number in the list is a percent of the way up the sorted data: 0% is the minimum, 50% is the median, and 100% is the maximum.

If `import numpy` gives a `ModuleNotFoundError` on your laptop, run `pip install numpy` in the terminal once.

**Learn more:** [NumPy: the absolute basics for beginners](https://numpy.org/doc/stable/user/absolute_beginners.html) (official) · [W3Schools: NumPy tutorial](https://www.w3schools.com/python/numpy/default.asp) · [W3Schools: Mean, median, and mode](https://www.w3schools.com/python/python_ml_mean_median_mode.asp)

## Words to know

Every number in this reading answers one of two questions: *what is typical?* or *how spread out are the values?*

### What is typical?: Measures of central tendency

**Typical** means usual or normal: the kind of value you'd expect to see most often. For example, if most guests gave between $40 and $75, a typical gift is somewhere in that range.

A **measure of central tendency** is one number that describes the typical value. *Central* means "in the middle," and *tendency* means "where values tend to gather." There are three.

| Word | What it means | Units |
| --- | --- | --- |
| **Mean** | Add every value, then divide by how many there are. Also called the average. One far-off value pulls it toward itself. | Same as the data (for gifts, dollars) |
| **Median** | The middle value once the values are sorted. With an even count, it's the average of the two middle values. One far-off value barely moves it. | Same as the data |
| **Mode** | The value that shows up most often. | Same as the data |

### How spread out?: Measures of spread

**Spread** means how far apart the values are. Gifts that are all close to $55 have a small spread. Gifts from $40 to $5,000 have a big spread. A **measure of spread** is one number that describes this.

| Word | What it means | Units |
| --- | --- | --- |
| **Range** | The largest value minus the smallest. | Same as the data |
| **Quartiles (Q1 and Q3)** | Values that split sorted data into four equal groups. Q1 is a quarter of the way up, the median is halfway, and Q3 is three quarters of the way up. | Same as the data |
| **Interquartile range (IQR)** | Q3 minus Q1: how spread out the middle half of the data is. Far-off values don't change it. | Same as the data |
| **Five-number summary** | The minimum, Q1, median, Q3, and maximum. It shows the spread without a chart. | Same as the data |
| **Variance** | Roughly the average of the *squared* distances between each value and the mean. Squaring makes every distance positive and makes big gaps count more. | Squared units (dollars squared), which are hard to picture |
| **Standard deviation** | The square root of the variance: the typical distance between a value and the mean. Small means the values sit close together. Large means they're spread out. | Same as the data |

{% hint style="info" %}
**Variance or standard deviation?** They measure the same spread. Variance comes out in squared units, like "dollars squared," which nobody can picture. Taking the square root puts it back in dollars. That's why reports give the standard deviation.
{% endhint %}

### What shape is the data?: Distribution and skew

| Word | What it means |
| --- | --- |
| **Distribution** | How the values are spread across their range: where most of them sit, and where only a few do. |
| **Histogram** | A bar chart where each bar counts how many values fall in a range. It shows a distribution's shape. |
| **Skew** | The way values lean. **Right-skewed** data has a long tail of big values, which pulls the mean above the median. **Left-skewed** data has a tail of small values, which pulls the mean below it. |
| **Outlier** | A value far from the rest. It can still be real. |

![Three histograms side by side. Each has an x-axis for the value, from small to big, and a y-axis for how many values. Left-skewed: most values are big, with a tail of small values on the left, and the mean sits below the median. Symmetric: one peak in the middle, and the mean and median are about the same. Right-skewed: most values are small, with a tail of big values on the right, and the mean sits above the median.](images/skew-shapes.svg)

## Before you read

In the reading, you'll focus on a fundraising dinner. Ten guests gave between $40 and $75, and one local company gave $5,000. The organizer wants to print "Our typical gift is ___" on next year's invitation.

Think about: which number would you print, and why? Write down your first answer, then see if the reading agrees.

## Read

As you read, look for:

1. Why the mean and the median give such different answers for the same gifts.
2. Which number in the five-number summary flags something unusual, and how you can tell.
3. Why the $5,000 gift stays in the data even though it pulls the mean up.

**[Start the reading: The Loudest Number in the Room →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/descriptive-statistics/reading-1-loudest-number/)** (about 20 minutes)

## Main takeaways

### Summary

* **Every number answers one of two questions:** what is typical (mean, median, mode), or how spread out are the values (range, IQR, standard deviation, five-number summary)?
* **Look at the shape, then pick the number.** On skewed data, the median describes a typical value better than the mean.
* **Keep a real outlier, and give units.** Report the median as typical, mention the outlier on its own line, and say what units each number is in.

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The mean uses every value, so it's always the most honest." | On skewed data, the mean gets pulled toward the tail and stops describing a typical value. |
| "Delete the outlier so the mean looks right." | A real value stays in the data. Pick the median instead, and name the outlier separately. |
| "A big standard deviation means the data has lots of variety." | It can also mean one far-off value. The five-number summary shows which one you have. |
| "Variance and standard deviation tell you different things." | They measure the same spread. The standard deviation is the square root of the variance, so it's in the data's own units. |

### How this connects

* **Next reading:** Instead of a short list you typed, you'll open a whole table of data saved in a file. Before you calculate anything, you'll check it: how many rows and columns it has, what kind of data each column holds, where values are missing, and whether any rows repeat. Then you'll keep only the rows you need.
* **Boss Battle (Module Project):** You'll describe key columns of a real dataset. For each one, you'll check its shape, pick the mean or the median, and explain its spread in plain words, with units.

## Quick check

**1.** Nine people at a small company earn between $45,000 and $60,000 a year. The owner earns $900,000. Which number should describe a typical salary?

<details>
<summary>Answer</summary>

The median. The owner's salary pulls the mean far above what almost everyone earns.

</details>

**2.** A column's mean is 30 and its median is 22. What does that suggest?

<details>
<summary>Answer</summary>

The data is right-skewed. A few big values pull the mean above the median, so the median is the better "typical" number.

</details>

---

**Next:** [Quest 2.2 — Look Before You Filter (Inspecting and Filtering Data)](quest-02-inspect-filter.md)
