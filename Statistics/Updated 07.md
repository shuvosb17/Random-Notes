## 🔗 Lecture 7: Correlation Analysis (Parts 1 & 2 Combined) — How Two Variables Move Together!

Welcome, data explorer! 🌟 So far, you’ve learned about the shape and spread of single variables — now it’s time to study **how two or more variables relate**. This chapter introduces **Correlation Analysis**, which helps us understand whether two things rise or fall together.

---

## 🎯 Learning Goals

By the end of this chapter, you will be able to:

* Define **Correlation** and understand its **types**.
* Learn visual and numerical methods for measuring correlation.
* Calculate **Karl Pearson’s coefficient (r)** and interpret its value.
* Understand **Spearman’s Rank Correlation** for non-numerical data.
* Apply correlation concepts to real-life situations in **business, economics, and research**.

---

## 🧠 1. What Is Correlation?

**Correlation** measures the **degree** (how strong) and **direction** (positive or negative) of relationship between two or more variables.

💡 In simple words: When one thing changes, does the other change too?

**Examples:**

* 🌦️ Temperature ↑ → Ice cream sales ↑ (Positive correlation)
* ⛽ Fuel price ↑ → Car usage ↓ (Negative correlation)
* 🎲 Shoe size ↔ Intelligence (No correlation)

**Visual Idea:**

```
Positive →   /  (r close to +1)
Negative →  \   (r close to -1)
No Relation → .  (r close to 0)
```

---

## 📊 2. Types of Correlation

| Type                     | Explanation                       | Example                  | Visual |
| ------------------------ | --------------------------------- | ------------------------ | ------ |
| **Positive Correlation** | Both variables increase together. | Income ↑ → Spending ↑    | ↗️     |
| **Negative Correlation** | One increases, other decreases.   | Price ↑ → Demand ↓       | ↘️     |
| **Zero Correlation**     | No relationship.                  | Shoe size & intelligence | ⚫      |

### Based on Number of Variables:

| Type                     | Meaning                                         | Example                               |
| ------------------------ | ----------------------------------------------- | ------------------------------------- |
| **Simple Correlation**   | Between 2 variables.                            | Height & weight                       |
| **Partial Correlation**  | Between 2 variables while keeping others fixed. | Income vs savings (fixed age)         |
| **Multiple Correlation** | Between one variable and a group of others.     | Sales vs price + advertising + income |

### Based on Relationship Shape:

| Type                        | Meaning                    | Visual |
| --------------------------- | -------------------------- | ------ |
| **Linear**                  | Straight-line relationship | 📈     |
| **Nonlinear (Curvilinear)** | Curved pattern             | 📉📈   |

---

## 🟩 3. Scatter Diagram Method

A **scatter diagram** is the easiest way to see correlation visually.

**Steps:**

1. Plot each pair of (X, Y) values on a graph.
2. Observe the general pattern.

**Interpretation:**

| Pattern                   | Type of Correlation |
| ------------------------- | ------------------- |
| Points rise together      | Positive            |
| Points fall together      | Negative            |
| Points scattered randomly | Zero                |

**Visual Example:**

```
Positive →  . .  .  .
            .  . . . .

Negative →  .     .
           .   .
         . .

No Corr → . .   .  . . .  .
```

💡 **Real-life Use:** Businesses compare **advertising vs sales** using scatter plots to see if ads actually increase sales.

---

## 📈 4. Karl Pearson’s Coefficient of Correlation (r)

The **Pearson’s r** is a mathematical measure of the **strength and direction** of a linear relationship between two variables.

### Formula:

[ r = \frac{\sum (X - \bar{X})(Y - \bar{Y})}{\sqrt{\sum (X - \bar{X})^2 \sum (Y - \bar{Y})^2}} ]

Where:

* **X, Y** = data values
* **\bar{X}, \bar{Y}** = means of X and Y

### Range:

[ -1 ≤ r ≤ +1 ]

| Value of r | Meaning          | Type                   |
| ---------- | ---------------- | ---------------------- |
| +1         | Perfect positive | Both increase together |
| −1         | Perfect negative | One rises, other falls |
| 0          | No correlation   | Unrelated              |

### Strength Scale:

| |r| Range | Strength |
|-------------|-----------|-----------|
| < 0.3 | Weak |
| 0.3–0.7 | Moderate |
| > 0.7 | Strong |

---

## 🧮 Example: Karl Pearson’s r

| X | 2 | 4 | 6 | 8 | 10 |
| - | - | - | - | - | -- |
| Y | 1 | 3 | 5 | 7 | 9  |

**Step 1:** Calculate means ((\bar{X}=6, \bar{Y}=5))
**Step 2:** Substitute into formula →
[ r = \frac{\sum (X - 6)(Y - 5)}{\sqrt{\sum (X - 6)^2 \sum (Y - 5)^2}} = 1.0 ]

✅ **Perfect Positive Correlation** — as X increases, Y increases equally.

**Visual Idea:**

```
Y ↑
|  *
| *
|*
|____ X →
```

💡 **Real-life Use:**

* Economics: Income & consumption.
* Business: Advertising & sales.
* Education: Study time & marks.

---

## 🔢 5. Spearman’s Rank Correlation (rs)

Used when data is **ordinal** (ranks) or **non-numerical**.

### Formula:

[ r_s = 1 - \frac{6 \sum d^2}{n(n^2 - 1)} ]

Where:

* **d** = difference between ranks of X and Y
* **n** = number of pairs

### Example:

| Student | Rank in Math | Rank in Science | d  | d² |
| ------- | ------------ | --------------- | -- | -- |
| A       | 1            | 2               | -1 | 1  |
| B       | 2            | 1               | 1  | 1  |
| C       | 3            | 3               | 0  | 0  |

[ r_s = 1 - \frac{6(2)}{3(9 - 1)} = 1 - \frac{12}{24} = 0.5 ]

💡 **Interpretation:** Moderate positive relationship — good math students often do well in science.

**Visual:**

```
High rank ↔ High rank → Positive
High rank ↔ Low rank → Negative
```

---

## ⚙️ 6. Properties of Karl Pearson’s r

| Property            | Description                        |
| ------------------- | ---------------------------------- |
| 1️⃣ Range           | −1 ≤ r ≤ +1                        |
| 2️⃣ Unit-free       | Independent of measurement units   |
| 3️⃣ Linearity       | Measures only linear relationships |
| 4️⃣ Symmetry        | r(X,Y) = r(Y,X)                    |
| 5️⃣ Mean connection | Depends on deviations from means   |

---

## 🧩 7. Advantages & Limitations

### ✅ Advantages:

* Simple and easy to calculate.
* Tells both direction and strength.
* Useful in forecasting trends.
* Works for all numeric data.

### ⚠️ Limitations:

* Works **only for linear relationships**.
* Can be **misleading with outliers**.
* Not suitable for **qualitative or ranked data** (use Spearman’s instead).

---

## 💼 8. Real-World Applications

| Field          | Example                  | Insight                              |
| -------------- | ------------------------ | ------------------------------------ |
| **Economics**  | Income vs consumption    | Higher income → higher spending      |
| **Business**   | Ads vs sales             | More ads → higher sales (usually!)   |
| **Education**  | Attendance vs marks      | More attendance → better performance |
| **Healthcare** | Exercise vs BP reduction | More exercise → lower BP             |
| **Finance**    | Stock A vs Stock B       | Portfolio diversification            |

**Visual Summary:**

```
Strong +ve → Tight upward line
Strong −ve → Tight downward line
Weak → Scattered dots
None → Random cloud
```

---

## 🧮 Quick Recap Table

| Concept                  | Formula                           | Range    | Meaning                     |
| ------------------------ | --------------------------------- | -------- | --------------------------- |
| **Pearson’s r**          | Σ(X−X̄)(Y−Ȳ) / √[Σ(X−X̄)²Σ(Y−Ȳ)²] | −1 to +1 | Linear correlation strength |
| **Spearman’s rs**        | 1 − 6Σd² / n(n²−1)                | −1 to +1 | Rank-based correlation      |
| **Positive Correlation** | r > 0                             |          | Both increase together      |
| **Negative Correlation** | r < 0                             |          | One rises, other falls      |
| **Zero Correlation**     | r ≈ 0                             |          | No linear link              |

---

### ✅ Final Thought

Correlation shows how two things move *together*. 📈
Whether comparing income and spending or ads and sales, **r** helps predict one from the other — but remember: **correlation ≠ causation!**
