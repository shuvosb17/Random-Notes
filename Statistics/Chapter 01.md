# Chapter 1 — Foundations of Statistics 📊
---

> “**Statistics is the art of learning from data — and the science of making decisions with it.**” — (Think of this as your chapter motto 🧭)

---

## 1) What **is** Statistics? — short answer & big picture 🧠

**Idea (concise):** Statistics is the discipline that helps you **collect**, **organize**, **summarize**, **visualize**, and **interpret** data so you can make better decisions.

**Two practical faces of statistics**

* **Descriptive statistics** — what the data *looks like*. (e.g., averages, graphs.)
  *Real life:* A café computes the average daily sales last month to decide staffing levels. ☕
* **Inferential statistics** — what the data *tells you about a bigger world* (population) using a sample.
  *Real life:* A poll of 1,000 voters estimates the candidate’s support across the whole country. 🗳️

**Quick tip:** Always ask: *Am I summarizing the data I have, or am I trying to generalize beyond it?* If the latter, sampling method and uncertainty matter.

---

## 2) Population vs Sample vs Parameter vs Statistic — crystal clear table ✅

| Term           |                                          What it means |            Notation (common)           | Real-life example                               |
| -------------- | -----------------------------------------------------: | :------------------------------------: | ----------------------------------------------- |
| **Population** |                            The full set you care about |                    —                   | *All* students at the university 🎓             |
| **Sample**     |                                   A subset you observe |                    —                   | 200 students randomly surveyed 📝               |
| **Parameter**  | A numeric property of the population (usually unknown) |         μ (mean), σ² (variance)        | True average exam score of every student 🧾     |
| **Statistic**  |                      A numeric summary from the sample | x̄ (sample mean), s² (sample variance) | Average score from the 200 surveyed students 📈 |

**Why this matters:** We *estimate parameters* (unknowns about the population) using *statistics* computed from a sample. Good sampling = trustworthy estimates.

**Common confusion → quick fix:**

* *Parameter* = fixed but unknown (population).
* *Statistic* = random (depends on chosen sample).

---

## 3) Variables — types, examples & when to use what 📚

### A. Qualitative (Categorical) — categories, no numeric arithmetic

* **Nominal (no order):** e.g., eye color, brand name, blood type.
  *Use:* counts, percentages, mode, bar/pie charts. 🟦🟧🟩
* **Ordinal (ordered categories):** e.g., satisfaction ratings (Low, Medium, High), education level.
  *Use:* median, percentiles, ordered bar charts. ⭐⭐⭐

### B. Quantitative (Numeric) — we can do arithmetic

* **Discrete (countable):** number of defects, number of children.
  *Real life:* Number of days a machine is down this month = 0,1,2... 🔧
* **Continuous (measurable):** height, time, temperature (in theory infinite precision).
  *Real life:* Time taken to deliver a package in hours (can be 2.3, 2.34...). 🚚

**Rule of thumb:** The type of variable determines what plots and summaries are valid. Don’t compute a mean of categories.

---

## 4) Levels of Measurement — what summaries make sense (and why) ⚖️

| Level        |                                  What it means | Examples                         | Appropriate summaries                      |
| ------------ | ---------------------------------------------: | -------------------------------- | ------------------------------------------ |
| **Nominal**  |                   Categories, no natural order | Programming language, blood type | Mode, frequency table, bar chart           |
| **Ordinal**  |    Categories with order but not equal spacing | Satisfaction: low/med/high       | Median, percentiles, ordinal plots         |
| **Interval** |     Numeric, equal intervals, **no true zero** | Celsius temperatures, IQ scores  | Mean, median, SD (but ratios meaningless)  |
| **Ratio**    | Numeric, equal intervals, **true zero exists** | Income, age, weight              | Mean, median, geometric mean, ratios valid |

**Real-life implication:**

* If data are **ordinal** (like customer satisfaction), prefer **median** over mean — distances between “low” and “medium” aren’t necessarily the same as between “medium” and “high.”
* If it's **ratio**, you can legitimately say “twice as much.” (E.g., $200 is twice $100.)

**Quick caution:** Temperature in Celsius is interval — saying “20°C is twice 10°C” is meaningless.

---

## 5) Sampling Methods — when to use which (with real examples) 🎯

### A. **Probability sampling** — each unit has a known chance of selection (preferred for inference)

1. **Simple Random Sampling (SRS)**

   * *How:* Every individual has equal chance (random numbers, lottery).
   * *Real life:* Selecting 300 customer IDs at random from a company database to estimate average satisfaction. ✅
   * *Pro:* Unbiased; supports classic formulas for confidence intervals.
2. **Systematic Sampling**

   * *How:* Pick every kᵗʰ person (e.g., every 10th visitor).
   * *Real life:* Inspect every 20th product on a production line. 🏭
   * *Watch out:* If there’s a hidden periodic pattern (e.g., every 20th product is different), bias may occur.
3. **Stratified Sampling**

   * *How:* Split population into homogeneous subgroups (strata), sample within each.
   * *Real life:* For a national survey, stratify by region (urban/rural) and sample each region proportionally. 🌍
   * *Pro:* More precise than SRS when strata differ.
4. **Cluster Sampling**

   * *How:* Randomly select whole clusters (groups) and sample everyone or sample within clusters.
   * *Real life:* Randomly choose 10 schools, then survey all students in those schools. 🏫
   * *Pro:* Cost-effective for geographically spread populations; *con:* usually less statistically efficient than stratified sampling.

### B. **Non-probability sampling** — selection probability unknown (exploratory, quick)

* **Convenience sampling:** survey whoever is available (e.g., shoppers in a mall). 🛍️
* **Purposive (judgmental):** choose specific people for a reason (experts). 👩‍🔬
* **Quota sampling:** fix quotas by subgroup but not randomly select within them.
* **Snowball sampling:** existing subjects recruit future subjects (useful for hidden populations). 🔄

**Real-life note:** Use **probability** samples when you must support claims about the larger population with measures of uncertainty (confidence intervals, p-values). Use **non-probability** for fast, low-cost exploratory work or when a sampling frame is not available.

---

## 6) Practical checklist — designing a good study ✅🧾

* Define your **population** clearly (who/what exactly).
* Choose a **variable** and confirm its level of measurement.
* Pick an appropriate **sampling method** — prioritize probability sampling when you need reliable inference.
* Decide **sample size** (larger → more reliable, but costlier).
* Plan **data collection** (clear question wording, avoiding bias).
* Pre-specify how you will **summarize and visualize** the data.

---

## 7) Common pitfalls & how to avoid them ⚠️

* **Confusing sample with population** → always label which you mean.
* **Using mean with skewed data** → report median too.
* **Biased sampling** (convenience/volunteer) → results won’t generalize.
* **Ambiguous variable type** (e.g., Likert scale treated as interval) → be explicit and justify choices.
* **Hidden periodicity in systematic sampling** → randomize starting point or use SRS.

---

## 8) Mini practice — check your understanding (2 quick questions) ✍️

1. You survey 150 commuters by asking whoever is at a bus stop at 8 AM. What sampling method is this? Is it likely to be biased? **(Answer: Convenience sampling; yes — biased toward early commuters.)**
2. Which measure should you prefer for household income: mean or median? **(Answer: Median — because income is typically skewed by very high earners.)**

---

## 9) Short glossary (two-line definitions) 📚

* **Sample frame:** a list from which you draw your sample (e.g., customer database).
* **Bias:** systematic error that consistently pushes estimates away from the truth.
* **Random error:** variability due to chance; reduced by larger sample size.
* **Outlier:** a value much farther from others; check whether it is real or an error.

---


