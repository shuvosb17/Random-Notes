# 📘 **Chapter 6 — Shape of the Distribution**

> “**Not all averages are created equal — sometimes, one side of your data carries the weight.**” ⚖️

---

## 🎯 Learning Outcomes

After this chapter, you can:
✅ Recognize **skewness** and **kurtosis**.
✅ Calculate their coefficients.
✅ Interpret distribution shape (symmetry and peakedness).

---

## 1️⃣ Shape of the Distribution 🎨

The “shape” of a dataset describes how values are spread around the mean.
Two numerical measures help describe shape:

| Measure      | Meaning                                                |
| ------------ | ------------------------------------------------------ |
| **Skewness** | Direction and extent of asymmetry (left or right skew) |
| **Kurtosis** | Degree of peakedness or flatness around the mean       |

---

## 2️⃣ Skewness — The Tilt of Data 📈

### ➤ Definition

Skewness measures lack of symmetry.
In a perfectly symmetric distribution: **Mean = Median = Mode**.

If these differ, the distribution is **skewed**.

### ➤ Direction of Skewness

| Type                        | Shape               | Tail         | Relation of Mean, Median, Mode | Example                |
| --------------------------- | ------------------- | ------------ | ------------------------------ | ---------------------- |
| **Positive (Right-Skewed)** | Tail on right       | Right longer | Mean > Median > Mode           | Income, housing prices |
| **Negative (Left-Skewed)**  | Tail on left        | Left longer  | Mean < Median < Mode           | Age at retirement      |
| **Symmetric**               | Balanced bell curve | —            | Mean = Median = Mode           | Normal distribution    |

---

### ➤ Karl Pearson’s Coefficient of Skewness (SKₚ)

[
SK_p = \frac{\text{Mean} – \text{Mode}}{σ}
]

* Range ≈ –3 to +3.
* SKₚ = 0 → Symmetric.
* 0 < SKₚ < 1 → Mild positive skew.
* 1 < SKₚ < 2 → Moderate.
* 2 < SKₚ < 3 → High.
  *(Negative values mirror these for left skew.)*

**Example:** SKₚ = –1.75 → Moderately left skewed.

---

### ➤ Moment Coefficient of Skewness (β₁)

[
β₁ = \frac{μ₃^2}{μ₂^3}
]

| β₁  | Interpretation    |
| --- | ----------------- |
| 0   | Symmetric         |
| > 0 | Positively skewed |
| < 0 | Negatively skewed |

---

## 3️⃣ Kurtosis — How Peaked or Flat? ⛰️

### ➤ Definition

**Kurtosis** measures the “peakedness” of a distribution relative to a normal bell curve.

### ➤ Types of Kurtosis

| Type            | Shape        | β₂ Value | Meaning                    |
| --------------- | ------------ | -------- | -------------------------- |
| **Leptokurtic** | Sharp peak   | > 3      | Data clustered around mean |
| **Mesokurtic**  | Normal curve | = 3      | Moderate peak              |
| **Platykurtic** | Flat top     | < 3      | Data spread out            |

### ➤ Formula

[
β₂ = \frac{μ₄}{μ₂^2}
]

---

## 4️⃣ Interpretation Summary Table 🧭

| Measure              | Statistic  | Indicator  | What it Means                            |
| -------------------- | ---------- | ---------- | ---------------------------------------- |
| Skewness (SKₚ or β₁) | Asymmetry  | – 3 to + 3 | 0 = symmetric, + right skew, – left skew |
| Kurtosis (β₂)        | Peakedness | ≈ 3 normal | > 3 = sharper, < 3 = flatter             |

---

## 5️⃣ Examples 🧮

### **Skewness Example**

Marks of 10 students: 15, 25, 48, 50, 65, 95, 18, 85, 75, 55.
→ Compute mean, mode, σ, then SKₚ = (Mean – Mode)/σ.
Interpret sign (+/–) for direction and magnitude for strength.

### **Kurtosis Example**

Reading hours (6 people): 3, 4, 2, 4, 6, 2, 5.
→ Calculate moments μ₂ & μ₄ then β₂ = μ₄ / μ₂².
If β₂ > 3 → leptokurtic (very peaked).

---

## 6️⃣ Visual Intuition 🎨

```
       /\         __        __
      /  \      _/  \_     /  \
  Leptokurtic  Mesokurtic  Platykurtic
```

Leptokurtic = tall & narrow peak; Platykurtic = wide & flat.

---

## 7️⃣ Summary & Comparison 📋

| Feature        | Skewness                  | Kurtosis                   |
| -------------- | ------------------------- | -------------------------- |
| Definition     | Asymmetry of distribution | Peakedness of distribution |
| Statistic      | β₁ or SKₚ                 | β₂                         |
| Range          | –3 to +3                  | Usually ≈ 0 to 10          |
| Interpretation | Direction (left/right)    | Sharp vs flat peak         |
| Normal Value   | 0                         | 3                          |

---

## 8️⃣ Practical Uses 💼

✅ **Finance:** Skewness helps detect asymmetric returns; Kurtosis signals risk of extreme events.
✅ **Quality Control:** Shape analysis reveals process deviation.
✅ **Education:** Distribution of marks shows fairness or bias of exams.

---

## 💬 Quote to Remember

> “**The mean shows the middle, but skewness and kurtosis show the story on each side of that middle.**” 📈

---

## 🧩 Exercises to Try

1️⃣ For marks 15, 25, 48, 50, 65, 95, 18, 85, 75, 55 → Compute SKₚ and interpret.
2️⃣ For reading times 3, 4, 2, 4, 6, 2, 5 → Compute β₂ and classify kurtosis.

---
