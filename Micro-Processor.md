# 📘 Complete Study Guide: Jump Instructions in 8086 Assembly

Let me break down **Jump Instructions** with beautiful visualizations and crystal-clear concepts for your exam tomorrow!

---

## 🎯 Prerequisites (5-minute crash course)

Before diving in, you need to understand:

### 1. **CPU Execution Flow (Normal vs Jump)**

```
Normal Execution (Sequential):
┌─────────────┐
│ Instruction 1│
└──────┬──────┘
       │ IP increments
┌──────▼──────┐
│ Instruction 2│
└──────┬──────┘
       │ IP increments
┌──────▼──────┐
│ Instruction 3│
└─────────────┘

With Jump (Non-Sequential):
┌─────────────┐
│ Instruction 1│
└──────┬──────┘
       │
┌──────▼──────┐
│  JMP LABEL  │──────┐
└─────────────┘      │ IP modified
┌─────────────┐      │
│ Instruction 3│ (SKIPPED)
└─────────────┘      │
       ┌─────────────┘
┌──────▼──────┐
│ LABEL: Inst │
└─────────────┘
```

### 2. **Flag Register (The Decision Maker)**

```
8086 Flag Register (16-bit):
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ - │ - │ - │ - │OF │DF │ IF│TF │SF │ZF │ - │AF │ - │PF │ - │CF │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
                   ↑           ↑   ↑       ↑       ↑
                   │           │   │       │       └─ Carry Flag
                   │           │   │       └───────── Parity Flag
                   │           │   └───────────────── Zero Flag
                   │           └───────────────────── Sign Flag
                   └───────────────────────────────── Overflow Flag
```

**Key Flags for Jumps:**
- **ZF (Zero Flag)**: Set (1) if result = 0
- **SF (Sign Flag)**: Set (1) if result is negative
- **CF (Carry Flag)**: Set (1) if unsigned overflow
- **OF (Overflow Flag)**: Set (1) if signed overflow
- **PF (Parity Flag)**: Set (1) if even number of 1-bits

### 3. **Signed vs Unsigned Numbers**

```
Same Bit Pattern, Different Interpretations:

Byte Value: 11111110

Unsigned: 254 (positive)
Signed:   -2  (negative, using 2's complement)

For 8-bit:
  Unsigned range: 0 to 255
  Signed range:   -128 to +127
```

---

## 📊 BIG PICTURE: Jump Instructions Overview

```
┌─────────────────────────────────────────────────────────┐
│              JUMP INSTRUCTIONS TAXONOMY                  │
└───────────────────────┬─────────────────────────────────┘
                        │
          ┌─────────────┴──────────────┐
          │                            │
   ┌──────▼────────┐          ┌────────▼─────────┐
   │ UNCONDITIONAL │          │   CONDITIONAL    │
   │     JUMP      │          │      JUMP        │
   └───────────────┘          └────────┬─────────┘
          │                             │
      ┌───▼───┐              ┌──────────┴──────────┐
      │  JMP  │              │                     │
      └───────┘    ┌─────────▼────────┐  ┌─────────▼────────┐  ┌─────────▼────────┐
                   │  SIGNED JUMPS    │  │ UNSIGNED JUMPS   │  │ SINGLE-FLAG JUMPS│
                   │  (SF, OF, ZF)    │  │   (CF, ZF)       │  │  (Individual)    │
                   └──────────────────┘  └──────────────────┘  └──────────────────┘
                   │ JG, JL, JGE, JLE │  │ JA, JB, JAE, JBE │  │ JZ, JNZ, JC, JNC │
                   │ JE, JNE          │  │ JE, JNE          │  │ JS, JNS, JO, JNO │
                   └──────────────────┘  └──────────────────┘  │ JP, JNP          │
                                                                 └──────────────────┘
```

---

## 🚀 Section 1: UNCONDITIONAL JUMP (JMP)

### **Concept:**
- **Always** jumps, no questions asked
- Like a `goto` statement in C
- Changes IP (Instruction Pointer) to point to the label

### **Visual Example:**

```assembly
MOV AX, 5       ; AX = 5
MOV BX, 3       ; BX = 3
JMP L1          ; Jump to L1 (unconditional)
MOV BX, 1       ; ← This line is SKIPPED!
L1: MOV BX, 4   ; BX = 4
```

**Step-by-step execution:**

```
Step 1: AX = 5, BX = ?
Step 2: AX = 5, BX = 3
Step 3: JMP L1 → IP now points to L1
Step 4: (MOV BX, 1 is NEVER executed)
Step 5: AX = 5, BX = 4 ✅ FINAL ANSWER
```

### **Memory Layout:**

```
Memory Address  Instruction
─────────────────────────────
0100h:          MOV AX, 5
0103h:          MOV BX, 3
0106h:          JMP L1      ┐
0109h:          MOV BX, 1   │ (Skipped)
010Ch:  L1:     MOV BX, 4   ← Jump target
```

---

## 🔀 Section 2: CONDITIONAL JUMPS (The Smart Decisions)

### **How They Work:**

```
┌─────────────────────────────────────────────────┐
│  Step 1: Execute an instruction (e.g., CMP)     │
│          that modifies flags                     │
└────────────────┬────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────┐
│  Step 2: CPU checks Flag Register               │
└────────────────┬────────────────────────────────┘
                 │
      ┌──────────┴──────────┐
      │                     │
┌─────▼──────┐      ┌───────▼──────┐
│ Condition  │      │  Condition   │
│   TRUE     │      │    FALSE     │
└─────┬──────┘      └───────┬──────┘
      │                     │
┌─────▼──────┐      ┌───────▼──────┐
│ Jump to    │      │  Continue    │
│  LABEL     │      │  next inst.  │
└────────────┘      └──────────────┘
```

### **Range Limitation:**

```
Conditional jumps are SHORT jumps:
        ←── 126 bytes ──┤CURRENT├── 127 bytes ──→
                        │  POS  │
        (Backward)      └───────┘    (Forward)
```

---

## 🔢 Section 3: SIGNED JUMPS (For Negative/Positive Numbers)

### **When to use:** Comparing **signed integers** (-128 to +127 for bytes)

### **Key Instructions:**

| Mnemonic | Meaning | Condition | Flags Checked |
|----------|---------|-----------|---------------|
| **JG**   | Jump if Greater | dest > src | ZF=0 AND SF=OF |
| **JL**   | Jump if Less | dest < src | SF ≠ OF |
| **JGE**  | Jump if Greater/Equal | dest ≥ src | SF = OF |
| **JLE**  | Jump if Less/Equal | dest ≤ src | ZF=1 OR SF≠OF |
| **JE**   | Jump if Equal | dest = src | ZF=1 |
| **JNE**  | Jump if Not Equal | dest ≠ src | ZF=0 |

### **Visual Example:**

```assembly
MOV AX, 5       ; AX = 5 (signed)
MOV BX, -3      ; BX = -3 (signed, stored as FFFDh in 2's complement)
CMP AX, BX      ; Compare AX and BX (5 - (-3) = 8, positive)
JG L1           ; Jump if AX > BX (signed)
MOV CX, 0       ; ← This is skipped
L1: MOV CX, 1   ; CX = 1 ✅
```

**Flag Analysis:**

```
CMP AX, BX  →  5 - (-3) = 8

Result: 0008h (positive, non-zero)
┌────────────────────────────┐
│ SF = 0 (positive result)   │
│ ZF = 0 (non-zero)          │
│ OF = 0 (no overflow)       │
└────────────────────────────┘

JG condition: ZF=0 AND SF=OF
              ✅    AND  ✅  → JUMP TAKEN!
```

---

## 🔢 Section 4: UNSIGNED JUMPS (For Positive Numbers Only)

### **When to use:** Comparing **unsigned integers** (0 to 255 for bytes)

### **Key Instructions:**

| Mnemonic | Meaning | Condition | Flags Checked |
|----------|---------|-----------|---------------|
| **JA**   | Jump if Above | dest > src | CF=0 AND ZF=0 |
| **JB**   | Jump if Below | dest < src | CF=1 |
| **JAE**  | Jump if Above/Equal | dest ≥ src | CF=0 |
| **JBE**  | Jump if Below/Equal | dest ≤ src | CF=1 OR ZF=1 |
| **JE**   | Jump if Equal | dest = src | ZF=1 |
| **JNE**  | Jump if Not Equal | dest ≠ src | ZF=0 |

### **Visual Example:**

```assembly
MOV AL, 10      ; AL = 10 (unsigned)
MOV BL, 15      ; BL = 15 (unsigned)
CMP AL, BL      ; Compare AL and BL (10 - 15 → borrow needed)
JB L2           ; Jump if AL < BL (unsigned)
MOV CL, 1       ; ← This is skipped
L2: MOV CL, 0   ; CL = 0 ✅
```

**Flag Analysis:**

```
CMP AL, BL  →  10 - 15 = -5 (needs borrow in unsigned)

Binary subtraction:
  00001010 (10)
- 00001111 (15)
-----------
  11111011 (251 unsigned, -5 signed with borrow)

┌────────────────────────────┐
│ CF = 1 (borrow occurred)   │
│ ZF = 0 (non-zero)          │
└────────────────────────────┘

JB condition: CF=1
              ✅  → JUMP TAKEN!
```

---

## 🚩 Section 5: SINGLE-FLAG JUMPS (Direct Flag Tests)

### **Based on ONE specific flag:**

| Mnemonic | Meaning | Condition |
|----------|---------|-----------|
| **JZ**   | Jump if Zero | ZF = 1 |
| **JNZ**  | Jump if Not Zero | ZF = 0 |
| **JC**   | Jump if Carry | CF = 1 |
| **JNC**  | Jump if No Carry | CF = 0 |
| **JS**   | Jump if Sign (negative) | SF = 1 |
| **JNS**  | Jump if No Sign (positive) | SF = 0 |
| **JO**   | Jump if Overflow | OF = 1 |
| **JNO**  | Jump if No Overflow | OF = 0 |
| **JP**   | Jump if Parity (even) | PF = 1 |
| **JNP**  | Jump if No Parity (odd) | PF = 0 |

### **Visual Example:**

```assembly
MOV AX, 5
SUB AX, 5       ; AX = 0
JZ L3           ; Jump if ZF=1 (result was zero)
MOV BX, 1       ; ← Skipped
L3: MOV BX, 2   ; BX = 2 ✅
```

---

## 🔍 Section 6: CMP Instruction (The Setup for Jumps)

### **What CMP Does:**

```
CMP destination, source

Internally computes: destination - source
BUT doesn't store the result!
ONLY updates flags!
```

### **Visual Comparison:**

```
SUB AX, BX          vs          CMP AX, BX
─────────────────────────────────────────────
Computes AX - BX    │           Computes AX - BX
Stores in AX        │           Doesn't store!
Updates flags       │           Updates flags
```

### **Example:**

```assembly
MOV AX, 10
MOV BX, 5
CMP AX, BX      ; 10 - 5 = 5 (internally)
                ; AX still = 10 ✅
                ; Flags: ZF=0, SF=0, CF=0
JG LABEL        ; Since 10 > 5 (signed), jump!
```

---

## 🎨 Complete Flow Diagram

```
┌──────────────────────────────────────────────────────────┐
│              TYPICAL CONDITIONAL JUMP FLOW               │
└────────────────────┬─────────────────────────────────────┘
                     │
          ┌──────────▼──────────┐
          │  MOV AX, value1     │
          │  MOV BX, value2     │
          └──────────┬──────────┘
                     │
          ┌──────────▼──────────┐
          │   CMP AX, BX        │  ← Flags updated!
          └──────────┬──────────┘
                     │
          ┌──────────▼──────────┐
          │   Jxx LABEL         │
          └──────────┬──────────┘
                     │
         ┌───────────┴───────────┐
         │                       │
    ┌────▼─────┐         ┌───────▼──────┐
    │Condition │         │  Condition   │
    │  TRUE    │         │    FALSE     │
    └────┬─────┘         └───────┬──────┘
         │                       │
    ┌────▼─────┐         ┌───────▼──────┐
    │ Jump to  │         │  Next inst.  │
    │  LABEL   │         │  executed    │
    └──────────┘         └──────────────┘
```

---

## 📝 Worked Examples

### **Example 1: Signed Comparison**

```assembly
MOV AX, 5
MOV BX, 2
CMP AX, BX
JG L1
MOV CX, 0       ; ← Skipped (since 5 > 2)
L1: MOV CX, 1   ; CX = 1 ✅
```

**Analysis:**
- CMP: 5 - 2 = 3 (positive, non-zero)
- Flags: ZF=0, SF=0, OF=0
- JG checks: ZF=0 AND SF=OF → ✅ Jump!
- **Final: CX = 1**

### **Example 2: Unsigned Comparison**

```assembly
MOV AL, 200
MOV BL, 100
CMP AL, BL
JA L2
MOV CL, 0       ; ← Skipped (since 200 > 100)
L2: MOV CL, 1   ; CL = 1 ✅
```

**Analysis:**
- CMP: 200 - 100 = 100 (no borrow)
- Flags: CF=0, ZF=0
- JA checks: CF=0 AND ZF=0 → ✅ Jump!
- **Final: CL = 1**

### **Example 3: Exercise from PDF**

```assembly
MOV AX, 5
MOV BX, 5
CMP AX, BX
JNE L3
MOV CX, 1       ; ← Executed (since 5 = 5, no jump)
L3: MOV DX, 2   ; DX = 2
```

**Analysis:**
- CMP: 5 - 5 = 0
- Flags: ZF=1
- JNE checks: ZF=0? → ❌ No jump!
- **Final: CX = 1, DX = 2**

---

## 🎯 One-Page Cheat Sheet

```
┌────────────────────────────────────────────────────────────────┐
│                    JUMP INSTRUCTION CHEAT SHEET                 │
├────────────────────────────────────────────────────────────────┤
│ UNCONDITIONAL                                                   │
│  JMP label  →  Always jump                                      │
├────────────────────────────────────────────────────────────────┤
│ SIGNED JUMPS (for -128 to +127)                                │
│  JG   →  >   (ZF=0 AND SF=OF)     JL   →  <   (SF≠OF)         │
│  JGE  →  ≥   (SF=OF)              JLE  →  ≤   (ZF=1 OR SF≠OF) │
│  JE   →  =   (ZF=1)               JNE  →  ≠   (ZF=0)          │
├────────────────────────────────────────────────────────────────┤
│ UNSIGNED JUMPS (for 0 to 255)                                  │
│  JA   →  >   (CF=0 AND ZF=0)      JB   →  <   (CF=1)          │
│  JAE  →  ≥   (CF=0)               JBE  →  ≤   (CF=1 OR ZF=1)  │
│  JE   →  =   (ZF=1)               JNE  →  ≠   (ZF=0)          │
├────────────────────────────────────────────────────────────────┤
│ SINGLE-FLAG JUMPS                                              │
│  JZ/JE  → ZF=1    JNZ/JNE → ZF=0    JC  → CF=1    JNC → CF=0  │
│  JS → SF=1    JNS → SF=0    JO → OF=1    JNO → OF=0           │
│  JP → PF=1    JNP → PF=0                                       │
├────────────────────────────────────────────────────────────────┤
│ CMP INSTRUCTION                                                 │
│  CMP dest, src  →  Compute (dest - src), update flags only     │
│  Original values unchanged!                                     │
├────────────────────────────────────────────────────────────────┤
│ KEY FORMULAS                                                    │
│  Signed overflow:  SF ≠ OF                                     │
│  Unsigned borrow:  CF = 1                                      │
│  Equal:            ZF = 1                                      │
└────────────────────────────────────────────────────────────────┘
```

---

## ✅ Practice Questions (Try Before Looking!)

### **Q1:**
```assembly
MOV AX, 10
MOV BX, 20
CMP AX, BX
JL L1
MOV CX, 5
L1: MOV CX, 10
```
What is CX? (Signed comparison)

<details>
<summary>Answer</summary>
CX = 10 (Jump taken since 10 < 20)
</details>

### **Q2:**
```assembly
MOV AL, 255
MOV BL, 1
CMP AL, BL
JB L2
MOV CL, 100
L2: MOV CL, 200
```
What is CL? (Unsigned comparison)

<details>
<summary>Answer</summary>
CL = 100 (No jump, since 255 > 1 unsigned)
</details>

### **Q3:**
```assembly
MOV AX, 0
SUB AX, AX
JNZ L3
MOV BX, 50
L3: MOV BX, 75
```
What is BX?

<details>
<summary>Answer</summary>
BX = 50 (No jump since ZF=1 after SUB, JNZ needs ZF=0)
</details>

---

## 🚀 Quick Exam Tips

1. **Always trace flags** after CMP or arithmetic ops
2. **Signed vs Unsigned:** Context matters!
   - Loop counters, array indices → Unsigned (JA/JB)
   - Temperature, bank balance → Signed (JG/JL)
3. **CMP doesn't change operands** — only flags!
4. **JE and JZ are identical** (same for JNE/JNZ)
5. **Remember the range:** ±126/127 bytes for conditional jumps

---

**Good luck on your exam! 🎓 You've got this!**

Would you like me to create a **printable PDF** with diagrams or focus on any specific section?
