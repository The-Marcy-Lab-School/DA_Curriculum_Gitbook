# Quest 2.1 — The Loudest Number: Descriptive Statistics (Day 1)

**Total time:** about 35 minutes

**EDA workflow:** Inspect → Clean → **Explore** → Check → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

**Why start at Explore?** You've already done some inspecting. In [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md), your function looked for invalid lines and caught blank values before you used them. But to judge a whole table, you need to know what "normal" looks like for each column. Is this value usual, or far from the rest? The mean, the median, and the spread answer that, so you learn them first, on a short list you can see all at once. In the next quest, you'll build on your inspecting skills and check a whole file. Then you can bring both skills together. ([Why the quests don't follow the step order](introduction.md#why-the-quests-dont-follow-the-step-order))

## Introduction

Sometimes averages can be misleading. For example, a street has ten homes. Nine sell for $300K each, and one large home sells for $3M. (K means thousand and M means million, so $300K is $300,000 and $3M is $3,000,000.)

To find the **average** (also called the **mean**), add up every value, then divide by how many values there are:

* Average = sum of all values ÷ number of values
* Average price = (9 × $300K + $3M) ÷ 10 = $5.7M ÷ 10 = **$570K**

But no home on that street sold for a price close to $570K. The one $3M home pulled the average up. If all ten homes sold for $300K, the average would be $300K, and it would describe every home.

![Two streets of ten houses. Left, one outlier: nine grey houses sold for $300K each, and one red house sold for $3M. Average = (9 × $300K + $3M) ÷ 10 = $5.7M ÷ 10 = $570K, and no house sold near $570K. Right, no outlier: ten grey houses sold for $300K each. Average = (10 × $300K) ÷ 10 = $300K, which matches every house.](images/average-outlier-houses.svg)

In this reading, you'll learn:

* when to use the average (the mean)
* when the middle value (the median) works better
* how to describe how spread out a set of numbers is

**Main takeaway:** An average can be misleading when the data has an outlier. An **outlier** is a value far from the rest, like the $3M home. Before you report an average, look at the shape of the data and check for outliers. When there is one, the middle value (the median) often describes the usual value better.

**Why it matters at work:** The number you report as "usual" (the mean, the median, or the mode) is the number people make decisions with. For example, teams use it to:

* set a budget, a plan for how much money to spend
* understand how much a customer usually spends
* set goals, like how many sales a team should make each month

If one outlier pulls that number up or down, those decisions are built on something that isn't true.

## Learning goals

After this reading, you should be able to say:

* I can find the mean, median, and mode, and explain which one describes "typical" for a set of numbers.
* I can describe how spread out data is with the standard deviation and the five-number summary, and say what units each one is in.
* I can tell whether data is skewed, and keep a real outlier while reporting it on its own.

**Skills:** Statistical Analysis · Data Distributions & Shape

## Quick recall

You've already added up numbers and read items by position. This reading uses both to describe a whole list with a few numbers.

* Recall that you added up a week of step counts with a running total (`total += steps`) in [One Job at a Time](../module-01/quest-07-second-function.md). An average goes one step further: divide the total by how many values there are, `sum(steps) / len(steps)`.
* Recall that you read a list item by its position, called its **index**, in [When the Crowd Grows](../module-01/quest-03-big-o-intuition.md). Python starts counting at 0, so `sorted_gifts[0]` is the first item and `sorted_gifts[1]` is the second. You'll use this to find the middle value of a sorted list.
* Recall that a **quantitative** value measures an amount, like a weight or a price. Math on it makes sense. You learned this in [What Kind of Data Is This?](../module-00/quest-02-data-literacy.md). An ID made of digits is not quantitative, so never take its mean.

## New Python package: NumPy

**What it's for:** NumPy does math on many numbers at once. Plain Python lists can add and count, but they don't have a median or a standard deviation built in. NumPy does, so each answer takes one line.

NumPy is a Python **package** (some people say *library*): a collection of code other people wrote. Recall that you loaded a **module** that comes with Python by writing `import json`, in [Make It Survive](../module-01/quest-05-serialization.md). You load a package the same way, with `import`. The difference: a package is a bigger set of modules, and it doesn't come with Python, so you install it yourself, once.

NumPy does its math on an **array**, not a list. An array is NumPy's version of a list, built for math:

| | List | Array |
| --- | --- | --- |
| **Comes from** | Python itself | NumPy, after `import numpy as np` |
| **What it holds** | Any mix of values, like `["Ana", 3, True]` | Values of one type, usually all numbers |
| **Math on every value** | Needs a loop | One step works on every value |
| **Example: `* 2`** | `[50, 40] * 2` repeats the list: `[50, 40, 50, 40]` | `np.array([50, 40]) * 2` doubles each value: `[100, 80]` |

**How you'll see it in this reading:**

```python
import numpy as np  # load the package

gifts = np.array([50, 40, 65, 50, 75, 45, 60, 50, 70, 55, 5000])

np.mean(gifts).round(2)         # 505.45
np.median(gifts)                # 55.0
np.std(gifts, ddof=1).round(2)  # 1490.71
np.percentile(gifts, [0, 25, 50, 75, 100])
```

<details>
<summary>Expand to walk through the code</summary>

1. `import numpy as np` loads the NumPy package and gives it the short name `np`.
2. `np.array([...])` turns the list of gifts into an array, so NumPy can do math on every gift at once.
3. `np.mean(...)` and `np.median(...)` are NumPy **functions** that find the mean and the median. `.round(2)` is a **method**, a function that belongs to the number NumPy gives back. It rounds that number to 2 decimal places.
4. `np.std(gifts, ddof=1)` finds the standard deviation. This line sets the parameter `ddof` to the argument `1`. You passed arguments to your own functions the same way in [Build It Once, Use It Again](../module-01/quest-02-functions-scope.md). That tells NumPy to use the **sample** formula, which divides by one less than the number of values. It's the version pandas and most other tools use, so your answers will match theirs.
5. `np.percentile(gifts, [0, 25, 50, 75, 100])` gives the five-number summary in one line. Each number in the list is a percent of the way up the sorted data: 0% is the minimum, 50% is the median, and 100% is the maximum.

</details>

If `import numpy` gives a `ModuleNotFoundError` on your laptop, run `pip install numpy` in the terminal once.

In class today, you'll run this code in a **Jupyter notebook**: a file that splits your code into small boxes called cells. For now, run the cells from top to bottom, one at a time. [Look Before You Filter](quest-02-inspect-filter.md#new-file-type-jupyter-notebooks) explains how notebooks work.

**Learn more:** [NumPy: the absolute basics for beginners](https://numpy.org/doc/stable/user/absolute_beginners.html) (official) · [W3Schools: NumPy tutorial](https://www.w3schools.com/python/numpy/default.asp) · [W3Schools: Mean, median, and mode](https://www.w3schools.com/python/python_ml_mean_median_mode.asp)

## Words to know

Every number in this reading answers one of two questions: *what is typical?* or *how spread out are the values?*

### What is typical?: Measures of central tendency

**Typical** means usual or normal: the kind of value you'd expect to see most often. For example, if most guests gave between $40 and $75, a typical gift is somewhere in that range.

A **measure of central tendency** is one number that describes the typical value. *Central* means "in the middle," and *tendency* means "where values tend to gather." There are three.

**Units** are what a number counts or measures, like dollars, minutes, or rows. Every number in these tables comes out in the same units as the data, except variance. The examples use the 11 gifts from the reading, sorted from smallest to biggest:

`40, 45, 50, 50, 50, 55, 60, 65, 70, 75, 5000` (in dollars)

| Word | What it means | Example with the gifts |
| --- | --- | --- |
| **Mean** | Add every value, then divide by how many there are. Also called the average. One far-off value pulls it toward itself. | $5,560 ÷ 11 = **$505.45** |
| **Median** | The middle value once the values are sorted. With an even count, it's the average of the two middle values. One far-off value barely moves it. | The 6th of 11 sorted gifts = **$55** |
| **Mode** | The value that shows up most often. | $50 shows up 3 times = **$50** |

### How spread out?: Measures of spread

**Spread** means how far apart the values are. For example:

* 9 gifts that are all about $50 have a **small** spread.
* 9 gifts where 2 are $50, 2 are $200, and 5 are $3,000 have a **big** spread.

A **measure of spread** is one number that describes this.

| Word | What it means | Example with the gifts |
| --- | --- | --- |
| **Range** | The largest value minus the smallest. | $5,000 − $40 = **$4,960** |
| **Quartiles (Q1 and Q3)** | Values that split sorted data into four equal groups. Q1 is a quarter of the way up, the median is halfway, and Q3 is three quarters of the way up. | Q1 = **$50**, Q3 = **$67.50** (NumPy's answer) |
| **Interquartile range (IQR)** | Q3 minus Q1: how spread out the middle half of the data is. Far-off values don't change it. | $67.50 − $50 = **$17.50** |
| **Five-number summary** | The minimum, Q1, median, Q3, and maximum. It shows the spread without a chart. | **$40, $50, $55, $67.50, $5,000** |
| **Variance** | Roughly the average of the *squared* distances between each value and the mean. Squaring makes every distance positive and makes big gaps count more. | Add up (each gift − $505.45)², then divide by 11 − 1 = about **2.2M dollars squared** |
| **Standard deviation** | The square root of the variance: the typical distance between a value and the mean. Small means the values sit close together. Large means they're spread out. | √2.2M = about **$1,490.71** |

The IQR is only $17.50, but the range is $4,960. That gap tells you one value sits far from the rest: the $5,000 gift.

{% hint style="info" %}
**Variance or standard deviation?** They measure the same spread. Variance comes out in squared units, like "dollars squared," which nobody can picture. Taking the square root puts it back in dollars. That's why reports give the standard deviation.
{% endhint %}

### What shape is the data?: Distribution and skew

| Word | What it means |
| --- | --- |
| **Distribution** | How the values are spread across their range: where most of them sit, and where only a few do. |
| **Histogram** | A bar chart where each bar counts how many values fall in a range. It shows a distribution's shape. |
| **Skew** | The way values lean. **Right-skewed** data has a long tail of big values, which pulls the mean above the median. **Left-skewed** data has a tail of small values, which pulls the mean below it. |
| **Outlier** | A value far from the rest, like the $3M home or the $5,000 gift. It can still be real. |

An outlier is not the same as a bad value. In [Validate, Catch, Keep Going](../module-01/quest-06-validation-errors.md), a grade of 14 broke a rule. So your function flagged it as a problem. A $5,000 gift breaks no rule. It's far from the rest, but it's real, so it stays in the data.

![Three histograms side by side. Each has an x-axis for the value, from small to big, and a y-axis for how many values. Left-skewed: most values are big, with a tail of small values on the left, and the mean sits below the median. Symmetric: one peak in the middle, and the mean and median are about the same. Right-skewed: most values are small, with a tail of big values on the right, and the mean sits above the median.](images/skew-shapes.svg)

## Before you read

In the reading, you'll focus on a fundraising dinner. A **fundraising dinner** is a meal where guests give money to support a cause. Ten guests gave between $40 and $75, and one local company gave $5,000. The organizer wants to print "Our typical gift is ___" on next year's invitation.

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
| "The mean uses every value, so it always represents the data well." | One outlier can pull the mean far from most values. The gifts' mean is $505.45, but 10 of the 11 gifts are $75 or less. |
| "Delete the outlier so the mean looks right." | A real value stays in the data. Pick the median instead, and name the outlier separately. |
| "A big standard deviation means the data has lots of variety." | It can also mean one far-off value. The five-number summary shows which one you have. |
| "Variance and standard deviation tell you different things." | They measure the same spread. The standard deviation is the square root of the variance, so it's in the data's own units. |

### How this connects

* **Next reading:** Instead of a short list you typed, you'll open a whole table of data saved in a file. Before you calculate anything, you'll check it: how many rows and columns it has, what kind of data each column holds, where values are missing, and whether any rows repeat. Then you'll keep only the rows you need.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** You'll describe key columns of a real dataset. For each one, you'll check its shape, pick the mean or the median, and explain its spread in plain words, with units.

## Quick check

**1.** Nine people at a small company earn between $45K and $60K a year. The owner earns $900K. Which number should describe a typical salary?

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

**Next:** [Quest 2.2 — Look Before You Filter: Inspecting and Filtering Data (Day 2)](quest-02-inspect-filter.md)
