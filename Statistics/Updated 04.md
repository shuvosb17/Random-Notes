## 📍 Lecture 4: Measures of Location (Part 1 & 2) — Finding Data Positions Made Fun!

Welcome back, data explorer! 🌟 You’ve mastered averages — now let’s find **where values sit** inside a dataset. This chapter is all about **location measures**, like quartiles, deciles, and percentiles — and how they help us see *spread and position*.

---

## 🎯 Learning Goals

By the end of this lesson, you will be able to:

* Understand and calculate **Quartiles (Q₁, Q₂, Q₃)**, **Deciles**, and **Percentiles**.
* Use these values to construct **Box and Whisker Plots**.
* Detect **outliers** using fences.
* Interpret and use **Interquartile Range (IQR)**.
* Connect everything to **real-world data analysis** (like salaries or exam results).

---

## 🧠 1. What Are Measures of Location?

Measures of location tell us **where** a specific value lies in a data set.

If “Measures of Central Tendency” (mean, median, mode) told us *the center*, then these tell us *the position*.

**Visual Idea:**

```
Lowest     Q1       Q2 (Median)       Q3       Highest
 |----------|-----------|-------------|-----------|
```

They help us know:

* How data is **spread** (range of values)
* Where the **middle 50%** of data lies
* If there are any **extreme (outlier)** values

---

## 🧩 2. Quartiles — Splitting Data into Four Parts

Quartiles divide ordered data into **four equal parts**.

| Quartile                | Position        | Meaning                |
| ----------------------- | --------------- | ---------------------- |
| **Q₁ (Lower Quartile)** | 25th percentile | 25% of data below it   |
| **Q₂ (Median)**         | 50th percentile | Half the data below it |
| **Q₃ (Upper Quartile)** | 75th percentile | 75% of data below it   |

### 📘 Formula (for grouped data):

[ Q_k = L + \left(\frac{\frac{kN}{4} - F}{f}\right) × c ]

Where:

* **L** = lower class boundary of the quartile class
* **N** = total frequency
* **F** = cumulative frequency before the class
* **f** = frequency of the class
* **c** = class width

### 🧮 Example:

Suppose marks of 40 students are grouped in a table. Using the formula, we can find:

* Q₁ = 25th percentile → tells where low performers end.
* Q₂ = 50th percentile → the median (middle score).
* Q₃ = 75th percentile → where top scorers begin.

**Visual Representation:**

```
|----Q1----|----Q2----|----Q3----|
25%        50%        75%
```

💡 **Real-life Use:**
Companies use **quartiles** to understand salary levels — lower, median, and upper ranges.

---

## 🔟 3. Deciles — Ten Equal Sections

Deciles divide data into **ten parts**.

| Symbol | Meaning                            |
| ------ | ---------------------------------- |
| **D₁** | 10% of data below                  |
| **D₅** | 50% of data below (same as median) |
| **D₉** | 90% of data below                  |

### Formula:

[ D_k = L + \left(\frac{\frac{kN}{10} - F}{f}\right) × c ]

💡 **Real-life Use:**
Used in **income distribution** — economists see how many people fall into the top or bottom 10%.

---

## 💯 4. Percentiles — Hundred Equal Parts

Percentiles break data into **100 parts**.

| Symbol  | Meaning        |
| ------- | -------------- |
| **P₅₀** | Median         |
| **P₂₅** | Q₁             |
| **P₇₅** | Q₃             |
| **P₉₀** | Top 10% cutoff |

### Formula:

[ P_k = L + \left(\frac{\frac{kN}{100} - F}{f}\right) × c ]

💡 **Real-life Use:**

* Exam results (e.g., SAT percentile ranks).
* Fitness reports (e.g., height/weight percentiles for children).

**Visual Idea:**

```
0%                 25%        50%        75%           100%
|------------------|----------|----------|--------------|
Lowest             Q1         Q2         Q3           Highest
```

---

## 📦 5. Box and Whisker Plot (Boxplot)

The **Boxplot** is a simple visual showing the **spread of data** — and helps us spot outliers easily!

### Steps to Create:

1. Arrange data in order.
2. Find **Minimum**, **Q₁**, **Median (Q₂)**, **Q₃**, and **Maximum**.
3. Draw a box from Q₁ to Q₃.
4. Draw a line in the box for the median.
5. Extend “whiskers” to the smallest and largest data within fences.

**Visual Example:**

```
|-----|==========|-----|
Min   Q1     Q2     Q3   Max
```

💡 **Real-life Use:**
Used in **salary analysis** — shows median salary, middle 50%, and who earns unusually high or low (outliers).

---

## 🚨 6. Detecting Outliers (Extreme Values)

Outliers are data points that lie **far away** from most others.

### Formulas:

* **Interquartile Range (IQR)** = Q₃ − Q₁
* **Lower Fence (Inner)** = Q₁ − 1.5 × IQR
* **Upper Fence (Inner)** = Q₃ + 1.5 × IQR
* **Outer Fences** = Q₁ − 3 × IQR and Q₃ + 3 × IQR

Any value **beyond inner fences** is a **mild outlier**, and beyond outer fences is an **extreme outlier**.

**Visual Idea:**

```
   |----o=========o----|
  Lower Outlier   Upper Outlier
```

💡 **Real-life Use:**

* Detecting **salary anomalies** — e.g., one employee earning far above average.
* Spotting **fraud or errors** in data.

---

## 📊 7. Interquartile Range (IQR)

The **Interquartile Range (IQR)** measures the **middle 50% spread** of data.

### Formula:

[ IQR = Q₃ − Q₁ ]

The **larger** the IQR, the more spread out the data.

**Example:**
If Q₃ = 80 and Q₁ = 40, then IQR = 80 − 40 = 40.

💡 **Real-life Use:**
Used to check **data consistency** — smaller IQR means more consistency.

**Visual Representation:**

```
|----Q1====(IQR)====Q3|
Smaller box → consistent data
Bigger box → more spread
```

---

## 🧩 8. Connecting It All: Boxplot Summary

| Term    | Meaning              | Formula        | Real-life Use              |
| ------- | -------------------- | -------------- | -------------------------- |
| Q₁      | 25th percentile      | (N/4)th value  | Lower boundary of data     |
| Q₂      | 50th percentile      | Median         | Middle of data             |
| Q₃      | 75th percentile      | (3N/4)th value | Upper boundary of data     |
| IQR     | Spread of middle 50% | Q₃ − Q₁        | Variability measure        |
| Outlier | Extreme value        | Beyond fences  | Detect unusual data        |
| Boxplot | Visual of all        | –              | Salary or score comparison |

---

## 💼 Real-World Example: Salary Analysis 💰

A company studies salaries of 100 employees.

| Step | Description      | Example Result                                    |
| ---- | ---------------- | ------------------------------------------------- |
| 1    | Arrange salaries | 20k – 200k                                        |
| 2    | Find Q₁, Q₂, Q₃  | 40k, 70k, 100k                                    |
| 3    | IQR = Q₃ − Q₁    | 100 − 40 = 60k                                    |
| 4    | Inner Fences     | 40 − 1.5(60) = −50 (ignore), 100 + 1.5(60) = 190k |
| 5    | Outliers         | Salaries > 190k                                   |

💡 **Interpretation:**
Only a few high-paid managers earn above 190k — visible as **outliers** in the boxplot.

**Visual Summary:**

```
20k |-----[=====|======|=====]-----| 200k
     Q1    Q2     Q3   Outliers
```

---

## 🧠 Quick Recap Table

| Concept     | What It Does         | Formula    | Used For            |
| ----------- | -------------------- | ---------- | ------------------- |
| Quartiles   | Split into 4 parts   | Q₁, Q₂, Q₃ | Middle spread       |
| Deciles     | Split into 10 parts  | D₁–D₉      | Detailed ranking    |
| Percentiles | Split into 100 parts | P₁–P₉₉     | Exam ranking        |
| Boxplot     | Visual summary       | –          | Salary, test scores |
| Outliers    | Detect extremes      | Fences     | Fraud/anomaly check |
| IQR         | Spread of middle 50% | Q₃ − Q₁    | Data consistency    |

---

### ✅ Final Thought

Measures of location help us **see the story behind the numbers** — where most data lies, where extremes appear, and how spread out everything is. Boxplots and quartiles make this story visible in one simple picture! 📦✨

---

📘 **Next Up:** **Chapter 5 – Measures of Dispersion** — How data spreads and varies from the center!
