# 🧠 MASTER NOTE: Branching & Jumping in Assembly (8086)

---

## 🔷 WHY WE NEED “JUMPS” & “BRANCHES”

In everyday life, you make decisions:

> “If it’s raining, take an umbrella, otherwise wear sunglasses.”

Computers must do the same — but CPUs can’t *“decide”*; they just follow instructions sequentially.
So, we use **jump** instructions to tell the CPU:
👉 *“Go somewhere else in the code if this condition is true.”*

This creates **branching**, i.e., multiple possible paths of execution.

---

# 🩵 PART 1 — JUMP INSTRUCTIONS

---

### 🧩 1. Unconditional Jump — `JMP`

🧠 **Meaning:** “Always go there — no questions asked.”

**Syntax**

```asm
JMP destination_label
```

### 🧍Real-Life Analogy:

Teacher says: “Skip the next question and go straight to question 5.”
No condition — just jump.

**Example:**

```asm
MOV AX, 5
MOV BX, 3
JMP L1      ; Go to L1, skip next instruction
MOV BX, 1   ; (This will NOT run)
L1: MOV BX, 4
```

### 🧾 Line-by-Line Explanation:

* `MOV AX,5` → Store 5 in AX register.
* `MOV BX,3` → Store 3 in BX register.
* `JMP L1` → CPU jumps to the label `L1`.
* `MOV BX,1` → skipped, because CPU already jumped.
* `L1: MOV BX,4` → executes this instruction finally.

**Result:** AX=5, BX=4
✅ *JMP is unconditional; it ignores everything else.*

---

### 🧩 2. Conditional Jump — `Jxxx`

🧠 **Meaning:** “Go there **only if** some condition is true.”

**Form**

```asm
CMP AX, BX
Jxx LABEL
```

1. `CMP AX, BX` → compares AX and BX by doing (AX − BX).

   * It doesn’t change AX or BX.
   * It only sets **flags** inside the CPU (Zero, Sign, Carry, Overflow).
2. `Jxx` → checks those flags to decide whether to jump.

---

### ⚙️ How It Works Internally

When you write:

```asm
CMP AX, BX
JG  L1
```

* If AX > BX (signed comparison), CPU jumps to label `L1`.
* Else, it continues to next line.

🧩 The CPU’s **flag register** works like traffic lights:

* ZF (Zero Flag): result = 0 → both equal
* SF (Sign Flag): result negative
* CF (Carry Flag): borrow/carry in unsigned math
* OF (Overflow Flag): signed overflow

---

### 🧮 3. Conditional Jump Types

#### a. **Signed jumps** (for negative/positive logic)

| Instruction | Meaning         | Example logic |
| ----------- | --------------- | ------------- |
| JL          | Jump if less    | if AX < BX    |
| JLE         | Jump if ≤       | if AX ≤ BX    |
| JG          | Jump if greater | if AX > BX    |
| JGE         | Jump if ≥       | if AX ≥ BX    |

**Example**

```asm
CMP AX, BX
JL SMALLER
; continues if AX ≥ BX
```

👉 *“Go to SMALLER if AX is less than BX.”*

---

#### b. **Unsigned jumps** (for positive-only numbers)

| Instruction | Meaning                | Example    |
| ----------- | ---------------------- | ---------- |
| JB          | Jump if below          | if AX < BX |
| JBE         | Jump if below or equal | ≤          |
| JA          | Jump if above          | >          |
| JAE         | Jump if above or equal | ≥          |

---

#### c. **Single flag jumps**

| Instruction | Jumps if...    | Example use     |
| ----------- | -------------- | --------------- |
| JZ          | Zero flag = 1  | if equal        |
| JNZ         | Zero flag = 0  | if not equal    |
| JC          | Carry flag = 1 | detect overflow |
| JNC         | Carry flag = 0 | no overflow     |
| JS          | Sign flag = 1  | negative result |
| JNS         | Sign flag = 0  | positive result |

---

### 🧠 Example: Compare Two Numbers

```asm
MOV AX, 5
MOV BX, 10
CMP AX, BX      ; AX − BX = -5 → SF=1
JL SMALLER      ; jump because AX<BX
MOV CX, AX
JMP END_
SMALLER:
MOV CX, BX
END_:
```

✅ CX = 10
💬 Like saying “if first number smaller → choose the other.”

---

# 💜 PART 2 — BRANCHING STRUCTURES

Now that we know jumps, let’s build *IF/ELSE/CASE* like in high-level languages (C, Python, etc.)

---

## 🔹 1. IF–THEN

**Logic in English:**
If AX < 0, replace it with –AX.

**Assembly:**

```asm
CMP AX, 0
JNL END_IF   ; Jump if not less (AX >= 0)
NEG AX       ; AX = -AX (only if AX<0)
END_IF:
```

### 🧾 Line-by-Line:

1. `CMP AX,0` → compares AX with 0 → sets flags.
2. `JNL END_IF` → if AX not less (≥0), skip the next line.
3. `NEG AX` → only runs when AX < 0 → flips sign.
4. `END_IF:` → continuation point.

🧍‍♂️ **Real-Life Example:**
“If balance < 0, convert it to positive.”
Otherwise do nothing.

---

## 🔹 2. IF–THEN–ELSE

**Logic:**
If AL < BL, show AL; else show BL.

**Assembly:**

```asm
MOV AH,2        ; for display
CMP AL,BL
JNBE ELSE_      ; Jump if AL > BL (unsigned)
MOV DL,AL       ; move smaller one to DL
JMP DISPLAY
ELSE_:
MOV DL,BL
DISPLAY:
INT 21H
END_IF:
```

### 🧾 Explanation:

* `CMP AL,BL` → compare.
* `JNBE ELSE_` → “Jump if not below or equal” → AL>BL.
* If jump doesn’t happen → AL ≤ BL → display AL.
* `MOV DL,AL` or `MOV DL,BL` → load ASCII for output.
* `INT 21H` → DOS interrupt for character display.

🧍‍♀️ **Real-Life Analogy:**
“If your test mark smaller, show it; otherwise show the other’s.”

---

## 🔹 3. CASE (Multi-Option Selection)

**Pseudocode:**

```
If AX < 0 → BX = -1
If AX = 0 → BX = 0
If AX > 0 → BX = 1
```

**Assembly:**

```asm
CMP AX, 0
JL NEG
JE ZERO
JG POS

NEG:  MOV BX, -1
      JMP END_CASE
ZERO: MOV BX, 0
      JMP END_CASE
POS:  MOV BX, 1
END_CASE:
```

### 🧾 Explanation:

* `CMP AX,0` → sets flags once.
* `JL`, `JE`, `JG` → three possible paths.
* `JMP END_CASE` → ensures only one path executes.

🧍‍♂️ **Real-Life Example:**
If temperature < 0 → “Freezing”
=0 → “Neutral”

> 0 → “Warm”

---

## 🔹 4. Compound Conditions

### a) **AND condition**

True when **both** are true.

**Example:** Display a character if it’s uppercase (‘A’–‘Z’).

```asm
MOV AH,1
INT 21H        ; read character → AL
CMP AL,'A'
JL END_IF      ; if AL<'A' → not uppercase
CMP AL,'Z'
JG END_IF      ; if AL>'Z' → not uppercase
MOV DL,AL
MOV AH,2
INT 21H
END_IF:
```

### 🧾 Explanation:

* Two comparisons → both must pass.
* Jump out early if any fails.
* Only when both succeed → display char.

🧍‍♀️ **Real-Life:** “If your age ≥18 AND have a license, you can drive.”

---

### b) **OR condition**

True if **any** is true.

**Example:** Display if char = ‘y’ or ‘Y’, else terminate.

```asm
MOV AH,1
INT 21H        ; read char
CMP AL,'y'
JE THEN
CMP AL,'Y'
JE THEN
JMP ELSE_
THEN:
MOV AH,2
MOV DL,AL
INT 21H
JMP END_IF
ELSE_:
; terminate
END_IF:
```

🧍‍♂️ **Real-Life:** “If you press ‘y’ or ‘Y’, continue — else exit.”

---

# 🌟 How It All Connects

| Concept            | English Meaning          | Assembly Tool             |
| ------------------ | ------------------------ | ------------------------- |
| Compare two values | if (a < b) / if (a == b) | `CMP` + Jump              |
| Decide one path    | if / else                | `Jxx` + labels            |
| Multiple choices   | switch / case            | multiple `Jxx`            |
| Combine conditions | AND / OR                 | sequence of `CMP` + `Jxx` |

---

# 🧩 PRACTICE PROBLEMS (10 + 10)

### 🩵 Jump Instructions (Week 5)

1. Write a program to check if AX == BX; if true → CX=1, else CX=0.
2. Compare AX and BX; if AX<BX, exchange their values.
3. If AX > 100 (unsigned), set BX=999; else BX=0.
4. If subtraction results in zero, jump to label EQUAL.
5. Use JNS to skip NEG AX if AX is already positive.
6. Add two numbers; if carry occurs, DX=1 else DX=0.
7. Test signed comparison: if AX<0, set BX=5 else BX=10.
8. If overflow occurs, clear AX to 0.
9. Demonstrate unconditional jump skipping two lines.
10. Using flags, detect even/odd number (hint: TEST AL,1 then JZ).

---

### 💜 Branching Structures (Week 6)

1. Replace negative AX with its absolute value.
2. Compare AL and BL; display smaller character.
3. Implement case: AX<0→BX=-1; AX=0→BX=0; AX>0→BX=1.
4. Read character; display if uppercase (‘A’-‘Z’).
5. Read char; display if ‘y’ or ‘Y’, else stop.
6. If (AL<10) AND (BL>5), store 1 in CL else 0.
7. If (AL==BL) OR (AL==CL), move 55h to DL.
8. Use CASE for 3 options: AX=1, AX=2, AX=3.
9. If BX<0, make positive; else add 5.
10. If AX>BX, CX=AX else CX=BX.

---

Excellent — that’s a *perfect “concept-integration” question*:
It combines **input**, **comparison (CMP)**, **conditional jumps**, and **output** — exactly the skills you’re expected to master.

Below are **5 similar questions**, each requiring an *IF–ELSE style assembly solution* with **conditional jumps**, all at the same reasoning level as your given example.

---

## 🧩 Question 1

### 👉 Problem Statement

Write an assembly language program using **IF–ELSE (with conditional jumps)** to take a number as input from the user and **display its ASCII code only if the number is greater than 3 and less than 7**.
Otherwise, do nothing.

🧠 **Concepts Used:**

* CMP instruction
* JBE / JAE for range checking
* Logical AND condition using two jumps
* INT 21h for input/output

---

## 🧩 Question 2

### 👉 Problem Statement

Write an assembly program that **takes a single character input**.
If it is a **lowercase letter (‘a’–‘z’)**, display the message `"Lowercase letter"`.
Otherwise, display nothing.

🧠 **Concepts:**

* `CMP AL, 'a'` and `CMP AL, 'z'`
* `JL` and `JG` to check range
* `AND` condition simulation via two jumps
* Display string via INT 21h

---

## 🧩 Question 3

### 👉 Problem Statement

Write an assembly program that **reads a character**.
If the character is **‘Y’ or ‘y’**, display the message `"You pressed YES"`.
Otherwise, display `"Program Terminated"`.

🧠 **Concepts:**

* OR condition (`JE` on two comparisons)
* Jumps for branching to `THEN` and `ELSE` blocks
* Multiple labels with JMP to structure the code

---

## 🧩 Question 4

### 👉 Problem Statement

Write an assembly program that **takes a signed number** in AX register.
If AX < 0, **convert it to its absolute value** and display `"Negative number converted"`.
Else, **display `"Number already positive"`**.

🧠 **Concepts:**

* Signed comparison → `JL`
* `NEG AX` to flip sign
* Two branches (IF and ELSE)
* Message display with INT 21h

---

## 🧩 Question 5

### 👉 Problem Statement

Write an assembly program that **reads two numbers** (say AL and BL).
If both numbers are **even**, display `"Both Even"`.
Otherwise, display `"At least one is odd"`.

🧠 **Concepts:**

* Use `TEST` instruction with 01h to check even/odd
* Compound condition using two comparisons (AND)
* `JNZ` (jump if not zero) for odd detection
* Nested IF–ELSE style control flow

---
Perfect! Let’s solve all 5 questions in a **concise, IF–ELSE style** assembly format using **conditional jumps** and **DOS interrupts**, keeping them in the **same style as your uppercase example**.

---

## 🧩 Question 1 – Number between 3 and 7

```asm
MOV AH,1
INT 21H            ; read number → AL
CMP AL,'3'
JLE END_IF         ; if AL <= '3', skip
CMP AL,'7'
JGE END_IF         ; if AL >= '7', skip
MOV DL,AL
MOV AH,2
INT 21H            ; display character
END_IF:
```

---

## 🧩 Question 2 – Lowercase letter check (‘a’-‘z’)

```asm
MOV AH,1
INT 21H            ; read character → AL
CMP AL,'a'
JL END_IF          ; if AL < 'a', skip
CMP AL,'z'
JG END_IF          ; if AL > 'z', skip
MOV DX, OFFSET MSG
MOV AH,09
INT 21H            ; display string "Lowercase letter"
END_IF:

MSG DB 'Lowercase letter$'
```

---

## 🧩 Question 3 – Check for ‘Y’ or ‘y’

```asm
MOV AH,1
INT 21H            ; read character → AL
CMP AL,'Y'
JE YES
CMP AL,'y'
JE YES
MOV DX, OFFSET NO
MOV AH,09
INT 21H            ; display "Program Terminated"
JMP END_IF

YES:
MOV DX, OFFSET YES_MSG
MOV AH,09
INT 21H            ; display "You pressed YES"

END_IF:

YES_MSG DB 'You pressed YES$'
NO      DB 'Program Terminated$'
```

---

## 🧩 Question 4 – Absolute value of signed number in AX

```asm
CMP AX,0
JGE POSITIVE       ; if AX >=0, skip NEG
NEG AX             ; AX = -AX
MOV DX, OFFSET MSG_NEG
MOV AH,09
INT 21H
JMP END_IF

POSITIVE:
MOV DX, OFFSET MSG_POS
MOV AH,09
INT 21H

END_IF:

MSG_NEG DB 'Negative number converted$'
MSG_POS DB 'Number already positive$'
```

---

## 🧩 Question 5 – Two numbers even check

```asm
MOV AH,1
INT 21H            ; read first number → AL
MOV BL,AL          ; store in BL
MOV AH,1
INT 21H            ; read second number → AL

TEST AL,1          ; check LSB of second number
JNZ ODD            ; if second number is odd, jump
TEST BL,1          ; check LSB of first number
JNZ ODD            ; if first number is odd, jump

; Both even
MOV DX, OFFSET BOTH
MOV AH,09
INT 21H
JMP END_IF

ODD:
MOV DX, OFFSET AT_LEAST
MOV AH,09
INT 21H

END_IF:

BOTH DB 'Both Even$'
AT_LEAST DB 'At least one is odd$'
```

---

### ✅ Notes on style and logic

1. **Input** always uses `AH=1 / INT 21H`.
2. **Output** uses `AH=2` for single character or `AH=09` for string.
3. **IF–ELSE logic** is implemented using:

   * `JL`, `JG`, `JE`, `JLE`, `JGE`, `JNZ` etc.
   * `JMP` to skip ELSE blocks when necessary.
4. **Compound conditions** (AND / OR) are simulated using multiple `CMP`/`TEST` + conditional jumps.

---


