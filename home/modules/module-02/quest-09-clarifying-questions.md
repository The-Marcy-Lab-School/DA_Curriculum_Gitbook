# Quest 2.9 — The Pattern Isn't the Proof: Asking Questions About Your Data (Day 10)

**Total time:** About 35 minutes

**EDA workflow:** Inspect → Clean → Explore → **Check** → Explain ([what's this?](introduction.md#the-big-picture-the-eda-workflow))

## Quick recall

You've checked a claim against its source, and you've counted blanks and group sizes. This reading turns those checks on the data file itself.

* In the interactive reading for [Drop, Fill, or Flag](quest-06-missing-data.md), `walks.isna().sum()` counted the blanks in a dog-walking log. Then you asked why each gap was missing, and whether the gaps were bunched in one group.
* One unusual value moves a small group's average a lot. So in [Beneath the Total](quest-08-mining-a-pattern.md), you checked how many rows each group had before trusting it.
* Module 0's [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md) had you check a chatbot's claim against a **source**: where information comes from. This time, you ask where the data file itself came from.

## Introduction

Sometimes a pattern in a file tells you more about how the data was collected than about the real world. For example, a review app (an app where people rate places) shows two neighborhoods. Each one has 8 restaurants. The app shows 4 highly rated restaurants in Northside, but only 1 in Riverside.

Maybe the food in Riverside is worse. Or maybe fewer people there use the app. Say the app gives a restaurant a rating only after it gets enough reviews:

* In Northside, many people use the app. All 8 restaurants have a rating, and 4 of those 8 are rated high.
* In Riverside, few people use the app. Only 2 restaurants have a rating, and 1 of those 2 is rated high.

In both places, half of the rated restaurants are rated high. Riverside shows fewer only because fewer of its restaurants got counted. In the picture below, look at the red restaurants in Riverside that have no rating.

![Two neighborhoods with 8 restaurants each. Left, Riverside, where few people use the review app: 6 restaurants are red because they have no rating, and only 2 have a rating. 1 of those 2 is rated high, so the app shows only 1 highly rated restaurant. Right, Northside, where many people use the app: all 8 restaurants have a rating, and 4 of those 8 are rated high. In both places, half of the rated restaurants are rated high.](images/restaurant-reviews-undercounted.svg)

**Main takeaway:** A pattern in a file can come from **bias** in how the data was collected, not from the real world. Bias here means some groups got counted less than others. For example, most of Riverside's restaurants had too few reviews to get a rating. Before you trust a pattern, ask **checkable questions** about where the data came from: questions specific enough that someone can answer them with a fact.

**Why it matters at work:** Analysts ask where data came from to make sure a pattern is real before anyone acts on it. For example, analysts ask these questions before:

* a city uses a survey to decide where to build a park
* a company uses sales data to decide which store to close
* a gym uses online sign-ups to cancel a class, when many people signed up on paper

If you skip this, money and effort go to the wrong place. For example, a park gets built where few people will use it.

## Learning goals

After this reading, you should be able to say:

* I can read a dataset's source note and name the questions it leaves open.
* I can check data for Origin, Completeness, and Bias, and count rows and blanks by group in code.
* I can turn a vague question into a checkable one that a data steward (the person who looks after the data) could answer.

**Skills:** Critical Thinking

## Words to know

### Where the data came from

The examples use the 16 restaurants from the Introduction. Each restaurant is one row. Its columns are the area and the rating. A restaurant with too few reviews has a blank rating. Here, any rating that isn't high is written as "low".

* Northside: `high, high, high, high, low, low, low, low`
* Riverside: `high, low, blank, blank, blank, blank, blank, blank`

Say the review file also comes with a short note from the app. (This note is added for these examples.) It says app users wrote the reviews over one year. It also says a restaurant gets a rating once it has "enough" reviews.

| Word | What it means | Example with the restaurants |
| --- | --- | --- |
| **Source note** | The short document that comes with a dataset. It says who collected the data, when, and how. Read it first. | It says app users wrote the reviews over one year. It never says how many reviews "enough" means. |
| **Data steward** | The person or team who looks after the data and can answer questions about it. | The app's data team, who keep the review file |
| **Sample** | The part of the whole that actually got counted. | The restaurants that got a rating: **8 of 8** in Northside, but only **2 of 8** in Riverside |

### The three-part checklist

| Word | What it means | Example with the restaurants |
| --- | --- | --- |
| **Origin** | Who collected this, and how? | Only app users wrote reviews, and fewer people in Riverside use the app. |
| **Completeness** | What's missing, and why? | **6 restaurants** have a blank rating, because they got too few reviews. |
| **Bias** | Who or what got **under-sampled**, meaning counted less than the rest? | Riverside: only **2 of 8** restaurants got a rating. In Northside, **8 of 8** did. |

The picture below puts the three questions in order, from a pattern to a checkable question.

![You find a pattern. Before you trust it, ask three questions. Origin: who collected this, and how? Completeness: what's missing, and why? Bias: who or what was counted less? Then write a checkable question that names a group, a number, or a method.](images/three-questions.svg)

### Asking good questions

| Word | What it means | Example with the restaurants |
| --- | --- | --- |
| **Checkable question** | A question specific enough that a data steward could answer it with a real fact. It names a group, a number, or a method, and ties to something you found. | "How many reviews does a restaurant need before the app shows a rating?" |
| **Generic question** | A question that could fit any dataset. It sounds careful, but nobody can answer it. | "Is this data accurate?" |

A generic question is like asking a chatbot "Are you sure?" In [Confidence Is Not Evidence](../module-00/quest-04-ai-verification.md), that got you a new claim, not a fact. A checkable question gets you a fact.

### Counting by group in code

Both lines below give back counts. **Units** are what a number counts. `.value_counts()` counts rows, and here each row is one restaurant. The second line counts blank cells. Say the file is loaded as a table called `places`.

| Word | What it means | Example with the restaurants |
| --- | --- | --- |
| **`.value_counts()`** | Lists each different value in a column with how many rows have it, biggest first. | `places["area"].value_counts()` gives Northside **8 restaurants** and Riverside **8 restaurants**. The rows look balanced. |
| **`places["rating"].isna().groupby(places["area"]).sum()`** | Counts the blanks in one column for each group of another column. `.isna()` marks each blank True, `.groupby(places["area"])` splits those by area, and `.sum()` adds them up. True counts as 1. | Riverside: False + False + 6 × True = 0 + 0 + 6 = **6 blank cells**. Northside: 8 × False = **0 blank cells**. |

You've used both tools before. `.value_counts()` showed "Kenya" spelled more than one way in [Write It Once](quest-07-cleaning-function.md). The `groupby` is the same split, apply, combine from [One Row Per Group](quest-03-group-columns.md), now on True/False values.

{% hint style="info" %}
**Who can answer it?** Some checkable questions the file can answer with code, like "How many Riverside restaurants have no rating?" Others only the source note or the data steward can answer, like "How many reviews does a restaurant need for a rating?"
{% endhint %}

## Before you read

In the reading, you'll focus on a street tree count. Volunteers counted trees in four parts of town, and the neighborhood association (a group of neighbors who work to improve their area) will plant new trees where the file shows the fewest. That's West, with only 2 trees.

Think about: does West really have the fewest trees, or could something else explain that number? Write down your first answer, then see if the reading agrees.

## ⭐ Read (REQUIRED)

As you read, look for:

1. What the source note answers, and what it leaves open.
2. Why a total of 4 blanks hides something that a count by group shows.
3. How to rewrite "Why is data missing?" into a question someone can answer.

**[Start the reading: The Pattern Isn't the Proof →](https://the-marcy-lab-school.github.io/DA_Curriculum_Readings/Mod2/interrogating-your-data/reading-1-the-pattern-isnt-the-proof/)** (about 20 minutes)

## Main takeaways

### Summary

* **Read the source note first.** It answers some questions and shows which ones are still open. The review app's note never says how many reviews "enough" means.
* **Check every dataset for Origin, Completeness, and Bias.** Count rows and blanks *by group* in code before you quote a number. Both areas have 8 rows. But 6 of Riverside's 8 restaurants have no rating, and none of Northside's are blank.
* **Ask checkable questions.** A good one names a group, a number, or a method, and a data steward could answer it with a fact.

| Generic (nobody can answer) | Checkable (a steward can answer) |
| --- | --- |
| "Is this data accurate?" | "How many reviews does a restaurant need before the app shows a rating?" |
| "Why is data missing?" | "6 of Riverside's 8 restaurants have no rating. How many reviews did each of those 6 get?" |

### Common mix-ups

| If you think... | What's actually true |
| --- | --- |
| "The app shows fewer highly rated restaurants in Riverside, so Riverside's food is worse." | A file shows what was collected. Only 2 of Riverside's 8 restaurants have a rating. 1 of those 2 is high: that's half, the same as Northside's 4 of 8. |
| "I'll ask, 'Is this data accurate?' That covers everything." | No single fact answers it, so the data steward can't answer it. "How many reviews does a restaurant need for a rating?" gets a real answer. |
| "Only 6 of the 16 restaurants are missing a rating, so the blanks don't matter much." | All 6 blanks are in Riverside. That's 6 of Riverside's 8 restaurants, so Riverside's ratings can't be compared with Northside's. |

### How this connects

* **Next reading:** You'll use the same habit on AI (artificial intelligence). You'll save a chart as an image, ask an AI chat to describe it, and check each thing it says against numbers you worked out yourself.
* **[Boss Battle (Module Project)](introduction.md#the-boss-battle-module-project):** Before you trust a pattern in a real dataset, you'll check where the data came from, what's missing, and who got counted less. Then you'll write checkable questions about it for someone who knows the data.

## Quick check

**1.** Next year, the app adds paper comment cards, but only in Riverside's restaurants. Now the app shows 3 highly rated restaurants in Riverside instead of 1. Which question goes to the data steward?

* A. "Is the comment card data reliable?"
* B. "Does a comment card count toward a rating the same way an app review does?"
* C. "Did Riverside's food get better?"

<details>
<summary>Answer</summary>

**B.** It's specific and checkable. A is generic, and C is the question the data can't answer until B is settled.

</details>

**2.** Name the three rows of the checklist.

<details>
<summary>Answer</summary>

Origin (who collected it, and how), Completeness (what's missing, and why), and Bias (who or what got counted less).

</details>

---

**Next:** [Quest 2.10 — Two Sets of Eyes: Checking AI on Charts (Day 11)](quest-10-ai-on-charts.md)
