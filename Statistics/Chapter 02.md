
# 📘 Chapter 2 — Frequency Distribution & Graphical Presentation

> “**Data tell their stories through patterns — your job is to make those patterns visible.**” 🌈

---

## 1️⃣ Understanding Frequency & Frequency Distributions

### 💡 **Core Idea:**

Raw data (individual observations) can be messy and overwhelming.
A **frequency distribution** groups data into categories or classes to show how often each value occurs.

---

### 🧮 **Types of Frequency Information**

| Type                          | Definition                        | Formula / How to find            | Real-life example                 |
| ----------------------------- | --------------------------------- | -------------------------------- | --------------------------------- |
| **Frequency (f)**             | Number of observations in a class | Count occurrences                | 8 students scored between 50 – 59 |
| **Relative frequency (rf)**   | Proportion of total in each class | rf = f / n                       | 8 / 40 = 0.20 → 20 % of students  |
| **Percentage frequency**      | Relative frequency in %           | rf × 100                         | 20 % scored between 50 – 59       |
| **Cumulative frequency (cf)** | Running total of frequencies      | Add frequencies up to that class | 20 students scored ≤ 59           |

---

### 🏠 **Real-life Example — Restaurant Ratings**

| Rating (★) | Frequency (f) | Relative % | Cumulative f |
| ---------- | ------------- | ---------- | ------------ |
| 1 ★        | 2             | 10 %       | 2            |
| 2 ★        | 4             | 20 %       | 6            |
| 3 ★        | 8             | 40 %       | 14           |
| 4 ★        | 4             | 20 %       | 18           |
| 5 ★        | 2             | 10 %       | 20           |

👀 *Interpretation:* 40 % of customers gave 3 ★ ratings; 90 % gave ≤ 4 ★.
*Use cumulative data to find medians or percentiles.*

---

## 2️⃣ Constructing a Frequency Table — Step-by-Step 🪜

When data are **quantitative and continuous**, group them into class intervals.

### ⚙️ Steps to Construct:

1. **Find the Range:** Max − Min.

   * Example: highest 70, lowest 45 → range = 25.
2. **Decide Number of Classes (k):**
   Use **Sturges’ Rule:**
   [
   k = 1 + 3.322 \log_{10}(n)
   ]
   For n = 20 → k ≈ 5 classes.
3. **Determine Class Width (h):**
   [
   h = \frac{\text{Range}}{k}
   ]
   Round up for convenience (here ≈ 5).
4. **Set Up Classes:** Equal-width intervals (e.g., 45–49, 50–54, 55–59, 60–64, 65–69).
5. **Count Frequencies (f)** and compute relative & cumulative frequencies.

---

### 🧾 Example — Students’ Test Marks

| Class Interval | Frequency (f) | Midpoint (xᵢ) | Relative Freq (%) | Cumulative f |
| -------------- | ------------- | ------------- | ----------------- | ------------ |
| 45 – 49        | 2             | 47            | 10 %              | 2            |
| 50 – 54        | 5             | 52            | 25 %              | 7            |
| 55 – 59        | 8             | 57            | 40 %              | 15           |
| 60 – 64        | 3             | 62            | 15 %              | 18           |
| 65 – 69        | 2             | 67            | 10 %              | 20           |

✔️ Always check that Σf = n = 20.

**Quick tip:** Use **inclusive boundaries** consistently (e.g., 45 ≤ x < 50).

---

## 3️⃣ Graphical Presentation — Turning Numbers into Pictures 🎨

| Graph Type                             | Data Type                 | Appearance                  | Real-life Use                |
| -------------------------------------- | ------------------------- | --------------------------- | ---------------------------- |
| **Bar Chart**                          | Categorical (Qualitative) | Separate bars               | Compare products, brands     |
| **Pie Chart**                          | Categorical               | Circle divided into sectors | Market share, survey results |
| **Histogram**                          | Quantitative (Continuous) | Adjacent bars               | Show distribution shape      |
| **Frequency Polygon**                  | Quantitative              | Line connecting midpoints   | Compare two data sets        |
| **Ogive (Cumulative Frequency Curve)** | Quantitative              | Rising S-curve              | Find medians, quartiles      |
| **Line Chart / Time Series**           | Quantitative vs Time      | Points joined by line       | Sales, temperature trends    |
| **Pictograph**                         | Categorical               | Icons or pictures           | Public reports, infographics |

---

### 🏙️ **Real-life Applications**

* **Retail:** Bar charts for product popularity 🛍️
* **Finance:** Histograms for income distribution 💰
* **Education:** Ogives to determine percentile cut-offs 🎓
* **Weather:** Line chart for temperature changes 🌡️

---

## 4️⃣ Bar Chart vs Histogram — Know the Difference ⚔️

| Feature     | **Bar Chart**  | **Histogram**       |
| ----------- | -------------- | ------------------- |
| Data Type   | Categorical    | Continuous numeric  |
| Bar Spacing | Bars separated | Bars touch          |
| X-axis      | Categories     | Class intervals     |
| Y-axis      | Frequency / %  | Frequency / density |
| Example     | Favorite fruit | Heights of students |

🍎 *A bar chart compares different fruits;*
📏 *a histogram shows how height measurements are distributed.*

---

## 5️⃣ Frequency Polygon & Ogive — Visualizing Distribution Shape 📈

### 🔹 **Frequency Polygon**

* Constructed by joining midpoints of histogram bars with straight lines.
* Add a zero-frequency class before and after to close the polygon.
* **Purpose:** Compare multiple distributions (e.g., males vs females test marks).

**Real-life:** Two different stores’ weekly sales distributions on one graph.

---

### 🔹 **Ogive (Cumulative Frequency Graph)**

* Plots cumulative frequency against the **upper class boundary**.
* **Rising curve** that never decreases.
* **Used to find:** median, quartiles, percentiles.

  * Draw horizontal line at n/2 to locate median.
  * Read value on x-axis.

**Real-life:** School administrator checks the 50th percentile of exam scores to set a passing mark.

---

## 6️⃣ Merits & Demerits of Graphical Methods ⚖️

| Merits ✅                      | Demerits ⚠️                       |
| ----------------------------- | --------------------------------- |
| Easy to interpret visually    | Can mislead if scale is distorted |
| Compare patterns quickly      | Exact values hard to read         |
| Highlights trends & outliers  | Not ideal for small datasets      |
| Attracts interest & attention | Needs proper labeling & scaling   |

**Quick tip:** Always start axes at zero and label both axes clearly to avoid misinterpretation.

---

## 7️⃣ Practical Example — Sales Data Visualization 🛒

| Product | Sales ($ ’000) |
| ------- | -------------- |
| Shoes   | 40             |
| Bags    | 25             |
| Watches | 20             |
| Jackets | 15             |

* **Bar Chart:** Compares total sales by category.
* **Pie Chart:** Shows relative contribution (%).
* **Pareto Chart:** (Bar + line for cumulative %) — reveals which products drive most revenue (80/20 rule).

---

## 8️⃣ Summary Cheat Table 🧾

| Concept                    | Formula / Rule          | Purpose                           |
| -------------------------- | ----------------------- | --------------------------------- |
| **Sturges’ Rule**          | k = 1 + 3.322 log n     | Decide number of classes          |
| **Class Width**            | h = Range / k           | Determine interval size           |
| **Relative Frequency**     | f / n                   | Compare proportions               |
| **Cumulative Frequency**   | Σ f                     | Find median or percentiles        |
| **Histogram vs Bar Chart** | Touching vs Gapped Bars | Correct graph choice by data type |

---

## 9️⃣ Common Mistakes & How to Avoid Them 🚫

❌ Using too few or too many classes → hides patterns.
✅ Use 5 – 20 classes (max ≈ √n rule).

❌ Overlapping or gapped class intervals → double-counting / missing data.
✅ Ensure contiguous classes (e.g., 45 – 49, 50 – 54).

❌ Inconsistent scale on graphs → misleading visuals.
✅ Start Y-axis at zero and use equal intervals.

❌ Using bar chart for continuous data / histogram for categories.
✅ Match chart type to variable type.

---

## 🔟 Quick Practice ✍️

**Q1:**
You have 50 students’ test scores (30 – 80).
1️⃣ Find range = 50.
2️⃣ Use Sturges: k ≈ 1 + 3.322 log 50 ≈ 7.
3️⃣ Class width ≈ 50 / 7 ≈ 7 → use width = 10 for simplicity.

**Q2:**
From the table below, draw a histogram & ogive and estimate the median.

| Class Interval | Frequency |
| -------------- | --------- |
| 30 – 39        | 3         |
| 40 – 49        | 7         |
| 50 – 59        | 10        |
| 60 – 69        | 6         |
| 70 – 79        | 4         |

✔️ Median ≈ value at 25th percentile (n/2 = 15th value).
Locate on ogive to estimate median ≈ 55–57.

---

## 🔖 Chapter 2 Glossary

| Term                  | Definition                              |
| --------------------- | --------------------------------------- |
| **Class Interval**    | Range of values grouped together        |
| **Midpoint**          | (Lower + Upper) / 2 of class            |
| **Sturges’ Rule**     | Rule-of-thumb to choose class count     |
| **Ogive**             | Graph of cumulative frequencies         |
| **Frequency Polygon** | Line graph connecting midpoints         |
| **Histogram**         | Adjacent bars showing data distribution |

---

## 💬 Quick Quote to Remember

> “**Graphs turn data into stories; tables make those stories exact.**” 📖

---
