# Tool Guide: NumPy

{% hint style="info" %}
**In one sentence:** NumPy is a free Python library that does math on a whole list of numbers in one step.
{% endhint %}

## Why analysts use it

Plain Python lists can add and count, but they don't have a median or a standard deviation built in. NumPy has these and many more, so one line gives you the answer. pandas, the table tool you'll start using on Day 2, is built on top of NumPy.

## What you'll learn about it in Module 2

| Where | What you'll do |
| --- | --- |
| Quest 2.1 (Day 1) | Turn a list into an array and find the mean, median, standard deviation, and five-number summary |
| Day 2 onward | pandas takes over. You'll still see NumPy's name in results like `np.int64(3)`, which is just the number 3. |

## The lines you'll use most

```python
import numpy as np                      # load NumPy and call it np

gifts = np.array([40, 50, 55, 60, 5000]) # an array: NumPy's version of a list
np.mean(gifts)                           # the mean (average)
np.median(gifts)                         # the median (middle value)
np.std(gifts, ddof=1)                    # the standard deviation (spread)
np.percentile(gifts, [0, 25, 50, 75, 100])  # the five-number summary
```

## Common first-day problems

| Problem | Fix |
| --- | --- |
| `ModuleNotFoundError: No module named 'numpy'` | Run `pip install numpy` in the terminal once. |
| Your standard deviation doesn't match pandas | Add `ddof=1`. pandas uses this version by default. |
| Your quartile is a little different from your hand math | Tools estimate quartiles in slightly different ways. Neither answer is wrong. Say which method you used. |

## Getting started resources

* [NumPy: the absolute basics for beginners](https://numpy.org/doc/stable/user/absolute_beginners.html) (official guide)
* [numpy.median](https://numpy.org/doc/stable/reference/generated/numpy.median.html) and [numpy.std](https://numpy.org/doc/stable/reference/generated/numpy.std.html) (official reference pages, with small examples)
* [Python's statistics module](https://docs.python.org/3/library/statistics.html) (the same math for plain lists, without NumPy)

---

**Next:** [Quest 2.1 — The Loudest Number](quest-01-descriptive-statistics.md)
