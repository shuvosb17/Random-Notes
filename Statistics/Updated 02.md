## 📊 Lecture 2: Frequency Distribution & Graphical Representation — Made Super Simple!

Welcome back! 🎉 Now that we know the basics of statistics, let’s learn how to **organize and show data** in a way that’s easy to understand — using **tables** and **graphs**.

---

## 🎯 Learning Goals

By the end of this lesson, you will be able to:

* Understand **frequency**, **relative frequency**, and **cumulative frequency**.
* Create and read **histograms**, **frequency polygons**, and **ogives**.
* Draw **bar charts** and **pie charts**.
* Use **Sturges’ Formula** to find the number of class intervals.
* Connect these ideas to **real-life uses** — like studying sales, weather, and exam marks.

---

## 🧮 1. What Is Frequency?

**Frequency** means how often something happens.

| Data (Scores) | 2 | 3 | 3 | 4 | 5 | 5 | 5 | 6 | 6 | 7 |
| ------------- | - | - | - | - | - | - | - | - | - | - |
| **Frequency** | 1 | 2 |   | 1 | 3 |   |   | 2 |   | 1 |

👉 **Example:**

* The number 5 appears 3 times → its frequency is **3**.

### 📊 Types of Frequency

| Type                     | Meaning                                  | Formula / Example                        | Real-Life Use                                 |
| ------------------------ | ---------------------------------------- | ---------------------------------------- | --------------------------------------------- |
| **Simple Frequency**     | How many times each value appears.       | 5 appears 3 times.                       | Counting students who scored each grade.      |
| **Relative Frequency**   | The percentage or fraction of the total. | Frequency ÷ Total × 100                  | What percent of people buy a certain product. |
| **Cumulative Frequency** | Adds up frequencies step by step.        | Add each frequency to the one before it. | Used in income levels or marks distribution.  |

### 📘 Visual Idea:

```
Scores: 2   3   4   5   6   7
Freq : 1   2   1   3   2   1
Cum. : 1   3   4   7   9  10
```

The last number in cumulative frequency = total data count.

---

## 🧩 2. Frequency Distribution Table

When we have *lots* of data, we group it into **class intervals**.

Example: Students’ marks out of 100

| Class Interval | Frequency |
| -------------- | --------- |
| 0 – 20         | 3         |
| 20 – 40        | 5         |
| 40 – 60        | 12        |
| 60 – 80        | 8         |
| 80 – 100       | 2         |
| **Total**      | **30**    |

### 🎨 Visual Representation:

```
Marks →  |■■■       (3)
          |■■■■■     (5)
          |■■■■■■■■■■■■  (12)
          |■■■■■■■■  (8)
          |■■        (2)
```

This shows how many students fall in each mark range.

---

## 📏 3. Sturges’ Formula (For Class Intervals)

When we don’t know how many classes to make, we use **Sturges’ Formula**:

[ K = 1 + 3.3 \log_{10} n ]

Where:

* **K** = number of classes (intervals)
* **n** = total number of data points

**Example:** If there are 100 data points:
[ K = 1 + 3.3(\log 100) = 1 + 3.3(2) = 7.6 \approx 8 \text{ classes} ]

👉 So we create about **8 intervals**.

**Real-life use:** Market researchers use this when dividing customer ages or incomes into neat class groups.

---

## 📈 4. Graphical Representation

Graphs help us **see patterns** in data quickly.

### 🟦 (a) Histogram

A **histogram** shows frequencies for continuous data. The bars **touch** each other — no gaps!

| Class Interval | Frequency |
| -------------- | --------- |
| 0 – 10         | 2         |
| 10 – 20        | 5         |
| 20 – 30        | 8         |
| 30 – 40        | 3         |

**Visual Idea:**

```
Frequency
  8 |        ████
  6 |      ██████
  4 |    ██████
  2 |  ████
     ---------------------->
      0  10  20  30  40
```

💡 **Real-life use:** Stores make histograms to see how many items sell within certain price ranges.

---

### 🔺 (b) Frequency Polygon

A **frequency polygon** connects the midpoints of histogram bars with straight lines.

**Steps:**

1. Find midpoint of each class.
2. Plot points (midpoint, frequency).
3. Join with straight lines.

**Visual Example:**

```
Freq
  8 |       /\
  6 |     /    \
  4 |   /        \
  2 | /            \
     -----------------> Midpoints
```

💡 **Real-life use:** Used to compare two sets of data — e.g., sales in January vs February.

---

### 📈 (c) Ogive (Cumulative Frequency Curve)

An **ogive** shows how data accumulates over time or range.

Two types:

* **Less than Ogive** – uses upper class boundaries.
* **Greater than Ogive** – uses lower class boundaries.

**Example:**

```
Marks ≤ 20 → 3
Marks ≤ 40 → 8
Marks ≤ 60 → 20
Marks ≤ 80 → 28
Marks ≤ 100 → 30
```

**Visual Idea:**

```
Freq
30 |                 ●
25 |              ●
20 |           ●
10 |      ●
 5 |  ●
   ---------------------> Marks
```

💡 **Real-life use:** To find **median** or **percentiles** (like the 50th percentile in test scores).

---

### 🟩 (d) Bar Chart

A **bar chart** shows data in separate bars (for *categories*, not numbers). Bars **do not touch**.

| Fruit  | Frequency |
| ------ | --------- |
| Apple  | 10        |
| Mango  | 5         |
| Banana | 8         |

**Visual Idea:**

```
Count
10 | ████ Apple
 8 | ███ Banana
 5 | ██ Mango
```

💡 **Real-life use:** To compare things like favorite food, brand popularity, etc.

---

### 🟠 (e) Pie Chart

A **pie chart** is a circle divided into slices that show proportions.

**Example:**
If 100 people choose snacks:

* Chips = 40
* Popcorn = 30
* Candy = 20
* Juice = 10

Then:
[ \text{Angle for Chips} = \frac{40}{100} \times 360 = 144° ]

**Visual:**

```
🍕 Chips (big slice)
🍿 Popcorn (medium)
🍬 Candy (small)
🥤 Juice (tiny)
```

💡 **Real-life use:** Companies use it to show **market share**.

---

## 🧠 5. Ogive & Polygon Interpretation

* The **Histogram** gives the picture of data distribution.
* The **Frequency Polygon** connects class frequencies — easy to compare datasets.
* The **Ogive** connects **cumulative frequencies** — helps find **median**, **percentiles**, or **cut-off marks**.

**Visual Summary:**

```
Histogram → Actual bars
Polygon  → Connects tops of bars
Ogive    → Smooth curve (cumulative)
```

---

## 💡 Real-World Application Example: Market Analysis

A toy company records how many kids bought toys at different price ranges.

| Price Range ($) | No. of Kids |
| --------------- | ----------- |
| 0–10            | 5           |
| 10–20           | 15          |
| 20–30           | 25          |
| 30–40           | 10          |
| 40–50           | 5           |

* **Histogram:** Shows where most kids spend (the peak = $20–30).
* **Polygon:** Helps compare toy sales across months.
* **Ogive:** Finds 50% mark (median spending).

📊 **Result:** Most customers buy mid-range toys, so company focuses there!

---

## 🧩 Quick Recap Table

| Concept              | Meaning                | Real-Life Use          |
| -------------------- | ---------------------- | ---------------------- |
| Frequency            | Count of events        | Counting votes, sales  |
| Relative Frequency   | Fraction or % of total | Market share %         |
| Cumulative Frequency | Running total          | Income or marks levels |
| Histogram            | Continuous data bars   | Sales distribution     |
| Polygon              | Connected midpoints    | Comparing trends       |
| Ogive                | Cumulative curve       | Median, percentiles    |
| Bar Chart            | Separate bars          | Survey results         |
| Pie Chart            | Circle slices          | Market share           |
| Sturges’ Formula     | Find class count       | Grouping large data    |

---

### ✅ Final Thought:

Graphs and frequency tables are like the **language of data** — they turn long lists of numbers into clear pictures you can *see* and *understand* instantly.

📈 **Next Up:**
**Chapter 3 – Measures of Central Tendency (Mean, Median, Mode)** — How to find the “center” of data easily!
