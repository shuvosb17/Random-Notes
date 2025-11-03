# 📘 Chapter 4 — Measures of Location & Box-and-Whisker Plot

> “**Statistics isn’t just about averages — it’s about finding where you stand among the numbers.**” 💡

---

## 🎯 Learning Outcomes

After finishing this chapter, you’ll be able to:
✅ Compute **quartiles, deciles, and percentiles**.
✅ Interpret these “location” measures in context.
✅ Construct and analyze **box-and-whisker plots**.
✅ Detect **outliers** and describe **data spread**.

---

## 1️⃣ What Are Measures of Location? 📍

They show **where a value lies** in a sorted dataset — the “position” rather than the “center.”
If the **median** splits the data into **two equal halves**,
then other measures (quartiles / deciles / percentiles) divide it into finer, equal-sized parts.

| Measure                  | Symbol | Divides Data Into … | # of Cut-Points | Typical Use                                              |
| ------------------------ | ------ | ------------------- | --------------- | -------------------------------------------------------- |
| **Quartiles (Q₁,Q₂,Q₃)** | Q      | 4 parts             | 3               | Divide into quarters                                     |
| **Deciles (D₁–D₉)**      | D      | 10 parts            | 9               | Divide into tenths                                       |
| **Percentiles (P₁–P₉₉)** | P      | 100 parts           | 99              | Compare relative rank (“You’re in the 90ᵗʰ percentile!”) |

---

## 2️⃣ Quartiles (Q₁,Q₂,Q₃) 🧮

### ➤ Concept

* **Q₁ (First Quartile):** 25 % of data ≤ Q₁
* **Q₂ (Second Quartile):** Median (50 %)
* **Q₃ (Third Quartile):** 75 % of data ≤ Q₃

**Formula for Position:**
[
j = \frac{i (n + 1)}{4} \quad (i = 1,2,3)
]

If *j* is not an integer, round up or interpolate between the nearest ranks.

### 🧾 Example

Data (sorted): 50, 64, 70, 78, 88, 94 (n = 6)

* **Q₁ pos = 1 × (6 + 1)/4 = 1.75 → ≈ 2ᵗʰ value = 64**
* **Q₂ pos = 3.5 → median = (70 + 78)/2 = 74**
* **Q₃ pos = 5.25 → ≈ 6ᵗʰ value = 94**

🔍 **Interpretation:** 25 % scored ≤ 64; half ≤ 74; 75 % ≤ 94.

---

## 3️⃣ Deciles (D₁ to D₉) 🔟

### ➤ Concept

Divide data into ten equal segments.

**Position Formula:**
[
j = \frac{i (n + 1)}{10}
]
where i = 1 to 9.

**Example:** D₅ ≈ Median; D₁ ≈ 10ᵗʰ percentile.

**Real Life:** Income distribution reports often show the bottom 40 % (via D₄) or top 10 % (via D₉).

---

## 4️⃣ Percentiles (P₁ to P₉₉) 💯

### ➤ Concept

Split data into 100 equal parts.
**P₅₀ = Median**, **P₂₅ = Q₁**, **P₇₅ = Q₃**.

**Formula for Position:**
[
j = \frac{i (n + 1)}{100}
]
where i = desired percentile.

**Example:** If P₆₈ = 48, then 68 % of observations are ≤ 48.

**Real Life:** Standardized tests (SAT, IELTS) use percentiles to rank scores.

---

## 5️⃣ Step-by-Step Procedure (for Quartiles, Deciles, Percentiles) 🪜

| Step | Action                                | Example                                                 |
| ---- | ------------------------------------- | ------------------------------------------------------- |
| 1️⃣  | Arrange data ascending order          | 6, 7, 8, 9, 10, 15, 16, 16, 20, 20, 23, 33, 50, 58, 104 |
| 2️⃣  | Compute position using formula        | For Q₃ → 3 × (15 + 1)/4 = 12ᵗʰ value = 33               |
| 3️⃣  | If position not integer → interpolate | E.g., between 8ᵗʰ and 9ᵗʰ value                         |
| 4️⃣  | Interpret results                     | 75 % ≤ 33; top 25 % > 33                                |

---

## 6️⃣ Interpretation of Quartiles & Percentiles 🧭

| Measure | Meaning                 | Everyday Analogy                             |
| ------- | ----------------------- | -------------------------------------------- |
| Q₁      | Lower 25 % threshold    | Students scoring below Q₁ need extra help 📚 |
| Q₂      | Median = 50 % threshold | Half the class scored above, half below 🎓   |
| Q₃      | Upper 25 % threshold    | Top performers 🏆                            |
| P₉₀     | 90 % below this point   | You’re in the top 10 % 🚀                    |

---

## 7️⃣ Box-and-Whisker Plot 📦

### ➤ Definition

A **Box-and-Whisker Plot (Boxplot)** is a graph summarizing five key numbers (five-number summary):

| Statistic      | Symbol | Meaning        |
| -------------- | ------ | -------------- |
| Minimum        | Min    | Smallest value |
| First Quartile | Q₁     | 25 % cut-point |
| Median         | Q₂     | Middle value   |
| Third Quartile | Q₃     | 75 % cut-point |
| Maximum        | Max    | Largest value  |

---

### 🧩 Construction Steps

1️⃣ Arrange data in ascending order.
2️⃣ Compute Q₁, Q₂ (Median), Q₃.
3️⃣ Find **IQR = Q₃ − Q₁** (Inter-Quartile Range).
4️⃣ Compute fences to spot outliers:

| Fence Type       | Lower Fence    | Upper Fence    |
| ---------------- | -------------- | -------------- |
| **Inner Fences** | Q₁ − 1.5 × IQR | Q₃ + 1.5 × IQR |
| **Outer Fences** | Q₁ − 3 × IQR   | Q₃ + 3 × IQR   |

5️⃣ Draw a box from Q₁ to Q₃ with a line at Q₂; extend “whiskers” to adjacent (non-outlier) values; mark outliers as dots or stars.

---

### 🧾 Example (from slide data)

**Monthly starting salaries (USD):**
2720, 2765, 2860, 2880, 2890, 2900, 2930, 2950, 2960, 3060, 3260, 3525

| Statistic | Value             |
| --------- | ----------------- |
| Q₁        | 2870              |
| Q₂        | 2915              |
| Q₃        | 3010              |
| IQR       | 140 (3010 − 2870) |
| Min       | 2720              |
| Max       | 3525              |

**Fences:**
Inner → 2660 to 3220  Outer → 2450 to 3430

💥 Outliers: 3260 (near upper inner fence) and 3525 (> upper outer fence).

---

### 🎨 Sketch Interpretation

```
 |----|====================|----|
  Min   Q1   Median   Q3    Max
```

Left whisker longer → **negative (skew left)** distribution.

---

### 📊 Uses of Boxplots

✅ Compare distributions (e.g., male vs female salaries).
✅ Identify outliers visually.
✅ Judge symmetry / skewness.
✅ See spread and center at a glance.

**Real Life Examples:**

* HR departments use boxplots to compare departmental salaries. 🏢
* Hospitals compare patient recovery times across treatments. 🏥

---

## 8️⃣ Interpreting Boxplots 🧠

| Observation                             | Meaning                        |
| --------------------------------------- | ------------------------------ |
| Median centered in box + equal whiskers | ≈ Symmetric distribution       |
| Median near bottom + long upper whisker | Positively skewed (right tail) |
| Median near top + long lower whisker    | Negatively skewed (left tail)  |
| Dots beyond fences                      | Potential outliers             |

---

## 9️⃣ Example Summary Table 📋

| Statistic                 | Formula         | Example Value |
| ------------------------- | --------------- | ------------- |
| Q₁                        | 25ᵗʰ percentile | 2870          |
| Q₂                        | Median          | 2915          |
| Q₃                        | 75ᵗʰ percentile | 3010          |
| IQR                       | Q₃ − Q₁         | 140           |
| Inner Fence (Lower/Upper) | Q₁ ± 1.5 IQR    | 2660 / 3220   |
| Outer Fence (Lower/Upper) | Q₁ ± 3 IQR      | 2450 / 3430   |
| Outliers Detected         | > 3220          | 3260, 3525    |

---

## 🔟 Common Mistakes & How to Avoid Them ⚠️

❌ Forgetting to sort data before finding quartiles.
✅ Always arrange in ascending order.

❌ Using mean instead of median in boxplots.
✅ Boxplot is based on five-number summary (Min, Q₁, Median, Q₃, Max).

❌ Drawing fences at wrong scale.
✅ Use same units as data and mark clearly.

---

## 🧩 Practice Task

**Construct a Box-and-Whisker Plot** for the data below and identify outliers:
3, 9, 10, 2, 6, 7, 5, 8, 6, 6, 4, 9, 22

👉 *Hint:* Sort, find Q₁, Q₂, Q₃, IQR, then fences. Expect 22 to appear as an outlier.

---

## 🧠 Quick Formula Cheat Sheet

| Concept             | Formula                     |
| ------------------- | --------------------------- |
| Quartile Position   | (j = \frac{i (n + 1)}{4})   |
| Decile Position     | (j = \frac{i (n + 1)}{10})  |
| Percentile Position | (j = \frac{i (n + 1)}{100}) |
| IQR                 | Q₃ − Q₁                     |
| Inner Fences        | Q₁ − 1.5 IQR, Q₃ + 1.5 IQR  |
| Outer Fences        | Q₁ − 3 IQR, Q₃ + 3 IQR      |

---

## 💬 Quote to Remember

> “**Percentiles tell you where you stand; boxplots show how everyone else stands around you.**” 📦

---

## ✅ Chapter Summary

* Measures of location identify relative positions (Q, D, P).
* Boxplots visualize five-number summaries and outliers.
* **IQR = Q₃ − Q₁** measures spread of the middle 50 %.
* Outliers lie beyond **1.5 × IQR** fences.
* The boxplot reveals skewness and dispersion at a glance.

---
=
