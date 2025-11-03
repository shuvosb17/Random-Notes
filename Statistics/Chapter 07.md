# 📘 Chapter 7 — Correlation Analysis

> “**Correlation shows how two things move together — but never says one caused the other.**” 🔗

---

## 🎯 Learning Outcomes

After completing this chapter, you’ll be able to:
✅ Understand the **concept of correlation**.
✅ Identify **types of correlation and their interpretation**.
✅ Construct and analyze **scatter plots**.
✅ Compute and interpret the **correlation coefficient (r)**.
✅ Explain its **properties, advantages and limitations**.

---

## 1️⃣ What Is Correlation? 📊

**Definition:** Correlation measures the **relationship and strength of association** between two or more variables.

| Example Pair                        | Possible Relationship                         |
| ----------------------------------- | --------------------------------------------- |
| Advertising spend (X₁) & Sales (Y₁) | Positive (+ ve) — more ads → more sales       |
| Price (X₂) & Demand (Y₂)            | Negative (– ve) — higher price → lower demand |
| Temperature & Ice-cream sales       | Positive                                      |
| Time spent on leisure & grades      | Negative                                      |

---

## 2️⃣ Types of Correlation ⚖️

| Type                 | Direction of Change                         | Diagram Shape (Conceptual) | Real-Life Example                  |
| -------------------- | ------------------------------------------- | -------------------------- | ---------------------------------- |
| **Positive**         | Both variables increase together            | Upward slope ↗️            | More study hours → higher marks 📚 |
| **Negative**         | One increases, the other decreases          | Downward slope ↘️          | More price → less demand 🛒        |
| **Zero correlation** | No consistent pattern                       | Scattered cloud ☁️         | Hair length vs IQ 🙂               |
| **Perfect positive** | Points on a straight upward line (r = +1)   | ↗                          | Height in cm vs Height in inches   |
| **Perfect negative** | Points on a straight downward line (r = –1) | ↘                          | Supply vs Price in fixed market    |

**Non-linear correlation:** Curved pattern (e.g., efficiency vs number of workers shows rising then falling trend).

---

## 3️⃣ Scatter Diagram Method 📈

**Steps to draw:**
1️⃣ Take one variable on X-axis and the other on Y-axis.
2️⃣ Plot each (X,Y) pair as a dot.
3️⃣ Observe overall trend (direction and form).

**Example (Glucose vs Age):**

| Age (x) | Glucose (mg/dl) (y) |
| ------: | ------------------: |
|      21 |                  65 |
|      25 |                  79 |
|      42 |                  75 |
|      43 |                  99 |
|      57 |                  87 |

➡ Dots rise as age increases → **positive correlation.**

---

## 4️⃣ Karl Pearson’s Coefficient of Correlation (r) 🧮

### ➤ Formula (standard form)

[
r = \frac{Σ (X_i - \bar{X})(Y_i - \bar{Y})}
{\sqrt{Σ (X_i - \bar{X})^2 ; Σ (Y_i - \bar{Y})^2}}
]

Where n = number of pairs.

Alternate computational formulas also exist using Σx, Σy, Σxy, etc.

---

### 🧾 Example — Textbook Pages vs Price

| Book               | Pages (X) | Price ($) (Y) |
| ------------------ | --------: | ------------: |
| Intro to History   |       500 |            84 |
| Basic Algebra      |       700 |            75 |
| Business Mgmt      |       800 |            99 |
| Intro to Sociology |       600 |            72 |

* (\bar X = 650,; \bar Y = 82.5)
* Using Pearson’s formula → **r = 0.511**

✅ **Interpretation:** Moderate positive association — more pages tend to cost slightly more.

---

### 🔢 Interpretation of r

|    r value    | Strength of Relationship | Type               |
| :-----------: | ------------------------ | ------------------ |
|       0       | No linear relation       | —                  |
|   0 → ± 0.3   | Weak                     | Low association    |
| ± 0.3 → ± 0.7 | Moderate                 | Noticeable pattern |
|  ± 0.7 → ± 1  | Strong                   | Tight linear trend |
|      + 1      | Perfect positive         | Points on ↑ line   |
|      – 1      | Perfect negative         | Points on ↓ line   |

**Remember:** Correlation does *not* imply causation — a third factor may drive both variables.

---

## 5️⃣ Properties of Correlation Coefficient 📚

1️⃣ Range → –1 ≤ r ≤ +1
2️⃣ Unit-free (pure number).
3️⃣ Measures **linear** relation only.
4️⃣ Applicable to **quantitative** data only.

---

## 6️⃣ Advantages ✅ and Limitations ⚠️

| Advantages                              | Limitations                  |
| --------------------------------------- | ---------------------------- |
| Easy to understand & calculate          | Detects only linear patterns |
| Indicates both direction & strength     | Fails for qualitative data   |
| Useful for forecasting & trend analysis | Sensitive to outliers        |
| Widely applied in economics, finance    | Does not prove causation     |

---

## 7️⃣ Practical Uses in Real Life 🌍

| Field       | Application                                   |
| ----------- | --------------------------------------------- |
| Economics   | Price vs Demand, Income vs Consumption        |
| Business    | Advertising vs Sales, Training vs Performance |
| Education   | Study Hours vs Exam Marks                     |
| Health      | Exercise Time vs Weight                       |
| Environment | Rainfall vs Crop Yield                        |

---

## 8️⃣ Practice Problems 🧠

1️⃣ **Age vs Weight**
| Age (x yrs) | 1.6 | 2.5 | 3.3 | 4.4 | 5.6 |
| Weight (y kg) | 12 | 15 | 16 | 17 | 20 |
→ Find r and interpret. Expect **strong positive correlation**.

2️⃣ **Height vs Weight of Men**
Heights (cm): 160 165 170 175 180 185
Weights (kg): 65.1 67.9 70.1 72.8 75.4 77.2
→ r ≈ close to 1  (strong positive).

3️⃣ **Distance from Stream (x)** vs **Insect Species (y)**
x: 2 5 8 11 14 17 22 33 39
y: 26 25 19 19 14 9 5 3 2
→ r ≈ negative (stronger distance → fewer species).

4️⃣ **Distance (km)** vs **Diesel Used (l)**
x: 90 150 230 310 390
y: 19.2 33.9 49.0 79.5 89.9
→ Positive r (close to 1): longer distance → more diesel.

---

## 9️⃣ Concept Summary Table 📋

| Concept                     | Formula / Interpretation                                           | Notes                             |
| --------------------------- | ------------------------------------------------------------------ | --------------------------------- |
| Correlation Coefficient (r) | (\frac{Σ(X–\bar X)(Y–\bar Y)}{\sqrt{Σ(X–\bar X)^2 Σ(Y–\bar Y)^2}}) | Linear association strength       |
| Range of r                  | –1 to +1                                                           | Closer to ± 1 = stronger relation |
| r > 0                       | Positive relationship                                              | ↑ X → ↑ Y                         |
| r < 0                       | Negative relationship                                              | ↑ X → ↓ Y                         |
| r = 0                       | No linear relation                                                 | Scatter points random             |
| Perfect correlation         | r = ± 1                                                            | Exact line fit                    |

---

## 🔟 Cautions When Interpreting Correlation 🚫

❌ High r does *not* mean X causes Y.
✅ Use scatter plots to check linearity before trusting r.
✅ Watch for outliers that inflate or suppress r.
✅ Avoid mixing unrelated groups in one calculation.

---

## 💬 Quote to Remember

> “**Correlation is a mirror of association — not the rope of cause.**” 🔗

---

## 🧠 Quick Checklist Before You Calculate r

☑ Both variables numeric and paired properly.
☑ Data entered accurately (no missing pairs).
☑ Plot a scatter diagram first to see pattern.
☑ Compute r and interpret sign (+/–) and magnitude (weak/moderate/strong).

---
