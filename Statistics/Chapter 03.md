# 📘 Chapter 3 — Measures of Central Tendency

> “**A single number can tell the story of a thousand data points — if you choose the right one.**” 💡

---

## 1️⃣ Ungrouped vs Grouped Data — How Your Data Is Organized 🗂️

| Type               | Description                                   | Example                              | Typical Use                           |
| ------------------ | --------------------------------------------- | ------------------------------------ | ------------------------------------- |
| **Ungrouped data** | Individual raw values listed                  | 45, 48, 50, 52, 55 …                 | Small samples (n < 30)                |
| **Grouped data**   | Values arranged into classes with frequencies | 45 – 49 (2 students), 50 – 54 (5), … | Large data (n > 30) → compact summary |

💭 *Think of “ungrouped” as individual voices, and “grouped” as the choir singing together.*

---

## 2️⃣ Measures of Central Tendency — The “Center” of Data 📍

**Purpose:** Each measure gives a single value that best represents the whole dataset.

| Measure            | Symbol  | Typical Use                    | Sensitive to Outliers? | Works with                |
| ------------------ | ------- | ------------------------------ | ---------------------- | ------------------------- |
| **Mean**           | x̄ or μ | General average                | ✅ Yes                  | Interval / Ratio          |
| **Median**         | M       | Middle value of ordered data   | ❌ No                   | Ordinal / Ratio           |
| **Mode**           | Mo      | Most frequent value            | ❌ No                   | Nominal / Ordinal / Ratio |
| **Geometric Mean** | GM      | Average growth rate            | ✅ Yes (slightly)       | Positive Ratio            |
| **Harmonic Mean**  | HM      | Averaging rates                | ✅ Yes                  | Positive Ratio            |
| **Weighted Mean**  | —       | Different importance of values | ✅ Yes                  | Ratio (if weights valid)  |

---

## 3️⃣ Arithmetic Mean (“the average”) 🧮

### 👉 **Formula**

* **Ungrouped:** [
  x̄ = \frac{Σx_i}{n}
  ]
* **Grouped:** [
  x̄ = \frac{Σ f_i x_i}{Σ f_i}
  ]
   where (x_i) = class midpoint.

### ✏️ **Example**

10 students scored: 45, 48, 50, 50, 52, 55, 58, 60, 62, 65
[
x̄ = \frac{45 + 48 + 50 + … + 65}{10} = 54.5
]

📊 *Interpretation:* The “balance point” of all scores = 54.5.

### ⚡ **Real life**

Average monthly electricity bill to forecast household expenses. 💡

**Quick tip:** Mean uses *all* data but is pulled by outliers (e.g., one bill = $500 will raise mean).

---

## 4️⃣ Median — The Middle Value 📏

### 👉 **Ungrouped Data**

1. Order data ascending.
2. If n odd → middle value.
3. If n even → average of two middle values.

[
Median = \frac{(n/2)^{th} + (n/2 + 1)^{th}}{2}
]

**Example:** Scores = 45, 48, 50, 50, 52, 55, 58, 60, 62, 65
Median = (5ᵗʰ + 6ᵗʰ)/2 = (52 + 55)/2 = 53.5

### 👉 **Grouped Data**

[
Median = L + \frac{(n/2 − C_f)}{f_m} × h
]
where

* L = lower limit of median class
* C_f = cumulative frequency before median class
* f_m = frequency of median class
* h = class width

**Example (slide data):** Median ≈ 53.5.

🧭 **Interpretation:** Half of students scored ≤ 53.5 and half ≥ 53.5.

📈 **Real life:** Median income is used instead of mean to avoid the effect of millionaires.

---

## 5️⃣ Mode — The Most Frequent Value ⭐

### 👉 **Definition:**

The value (or class) that occurs most often.

### 👉 **Formula (for Grouped Data):**

[
Mode = L + \frac{d_1}{d_1 + d_2} × h
]
where

* d₁ = fₘ − fₚ  (prev class)
* d₂ = fₘ − fₙ  (next class)
* L = lower limit of modal class
* h = class width

**Example:** If modal class = 50 – 54, then Mode ≈ 52.5 (approx.)

🎯 **Real life:** Most common shoe size sold by a store → guides inventory.

**Quick tip:** Nominal data (e.g., eye color) → only Mode is meaningful.

---

## 6️⃣ Geometric Mean (GM) 📈

### 👉 **Formula**

[
GM = \sqrt[n]{x_1 × x_2 × … × x_n}
]
or using logs:
[
GM = antilog\left(\frac{Σ log x_i}{n}\right)
]

### ✏️ **Example**

For marks 45–65 (from Chapter 3 data): GM ≈ 54.15.

**Quick tip:** Only for positive values. Cannot include zero or negative.

### 🏦 **Real life**

Used for average growth rates (e.g., investment returns, population growth).
If a stock grows 10 %, 20 %, −5 %, the GM shows true average growth per year.

---

## 7️⃣ Harmonic Mean (HM) 🚗

### 👉 **Formula**

[
HM = \frac{n}{Σ (1/x_i)}
]

### ✏️ **Example**

Two trips of equal distance: 60 km/h out, 40 km/h back.
[
HM = \frac{2}{(1/60 + 1/40)} = 48 \text{ km/h}
]
→ Correct average speed = 48 km/h (not 50 km/h).

**Real life:** Used when averaging rates (speed, efficiency, density).

**Quick tip:** Heavily weights smaller values → use when rates are reciprocal of interest.

---

## 8️⃣ Weighted Mean 🎯

### 👉 **Formula**

[
\text{Weighted Mean} = \frac{Σ w_i x_i}{Σ w_i}
]
where w = weight (importance, frequency).

### ✏️ **Example**

| Grade | Points (x) | Credit (w) | w × x |
| ----- | ---------- | ---------- | ----- |
| A     | 4          | 3          | 12    |
| B     | 3          | 4          | 12    |
| C     | 2          | 2          | 4     |
| **Σ** | —          | 9          | 28    |

Weighted Mean = 28 / 9 ≈ **3.11 GPA** 🎓

**Real life:** Used in GPA calculation, price indices, and quality control.

---

## 9️⃣ Choosing the Right Measure 🧭

| Situation                      | Best Measure         | Why                                |
| ------------------------------ | -------------------- | ---------------------------------- |
| Data with outliers (salaries)  | **Median**           | Resistant to extremes              |
| Nominal data (colors, brands)  | **Mode**             | Only categorical choice            |
| Symmetric numeric data         | **Mean**             | Uses all values                    |
| Skewed distribution            | **Median** (or Mode) | Less distorted                     |
| Growth rates / percent changes | **Geometric Mean**   | Correct for multiplicative changes |
| Rates (average speed, density) | **Harmonic Mean**    | Suitable for reciprocal data       |
| Weighted importance            | **Weighted Mean**    | Reflects different significance    |

---

## 🔟 Merits & Demerits — Quick Comparison Table ⚖️

| Measure            | Merits ✅                   | Demerits ⚠️                |
| ------------------ | -------------------------- | -------------------------- |
| **Mean**           | Easy, uses all data        | Distorted by outliers      |
| **Median**         | Not affected by extremes   | Ignores magnitudes         |
| **Mode**           | Simple, works for nominal  | May be non-unique or vague |
| **Geometric Mean** | Best for rates of change   | Fails if zeros/negatives   |
| **Harmonic Mean**  | Useful for averaging rates | Sensitive to small values  |
| **Weighted Mean**  | Reflects importance levels | Requires valid weights     |

---

## 🧮 Formula Cheat Table 📋

| Measure             | Formula                                                         | Common Use                           |
| ------------------- | --------------------------------------------------------------- | ------------------------------------ |
| **Arithmetic Mean** | (x̄ = Σx_i / n)  or (Σ f x / Σ f)                               | General average                      |
| **Median**          | Ungrouped: Middle value    Grouped: (L + ((n/2 − C_f)/f_m) × h) | Skewed data                          |
| **Mode**            | (L + (d_1/(d_1 + d_2)) × h)                                     | Most common category                 |
| **Geometric Mean**  | ((Πx_i)^{1/n})                                                  | Growth rates                         |
| **Harmonic Mean**   | (n / Σ(1/x_i))                                                  | Average of rates                     |
| **Weighted Mean**   | (Σ w_i x_i / Σ w_i)                                             | Weighted averages (GPA, price index) |

---

## 💬 Quick Quote to Remember

> “**The mean tells you the story of the whole group, but the median reveals its balance.**” 📊

---

## 🧠 Practice Check ✍️

1️⃣ Compute the mean, median & mode for: 12, 15, 18, 20, 20, 21, 25.

* Mean = 18.7  Median = 20  Mode = 20.

2️⃣ A car travels 60 km at 40 km/h and 60 km back at 60 km/h.
→ Find average speed using HM.
[
HM = \frac{2}{(1/40 + 1/60)} = 48 \text{ km/h}
]

---

## 📚 Chapter 3 Glossary

| Term                 | Definition                       |
| -------------------- | -------------------------------- |
| **Central Tendency** | Typical or central value of data |
| **Outlier**          | Observation far from others      |
| **Mean**             | Arithmetic average               |
| **Median**           | Middle position value            |
| **Mode**             | Most frequent value              |
| **Weighted Mean**    | Average adjusted by importance   |
| **Harmonic Mean**    | Average of rates (reciprocals)   |
| **Geometric Mean**   | Mean based on product of values  |

---

## 🏁 Summary Snapshot

* Mean = uses all data but sensitive to extremes.
* Median = better for skewed data and ordinal data.
* Mode = for categorical data or most common item.
* Geometric Mean = for growth rates (%, ratios).
* Harmonic Mean = for speeds / rates.
* Weighted Mean = for importance-based averages.
