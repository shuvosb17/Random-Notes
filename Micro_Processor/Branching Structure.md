# 📘 Complete Study Guide: Branching Structures in 8086 Assembly

---

## 🎯 Prerequisites (Quick Review)

Before diving in, make sure you understand:

### 1. **Control Flow Basics**

```
Linear Execution (No Branching):
┌─────────────┐
│ Statement 1 │
└──────┬──────┘
       │
┌──────▼──────┐
│ Statement 2 │
└──────┬──────┘
       │
┌──────▼──────┐
│ Statement 3 │
└─────────────┘

Branching (Decision Making):
┌─────────────┐
│   Decision  │
└──────┬──────┘
       │
  ┌────┴────┐
  │         │
┌─▼──┐   ┌──▼─┐
│Path│   │Path│
│ A  │   │ B  │
└────┘   └────┘
```

### 2. **Conditional Jump Review (from your previous lecture)**

```
Key Instructions You'll Use:
JL  → Jump if Less (signed)
JLE → Jump if Less or Equal
JG  → Jump if Greater (signed)
JGE → Jump if Greater or Equal
JE  → Jump if Equal
JNE → Jump if Not Equal
JMP → Unconditional Jump
```

### 3. **Comparison Direction**

```
CMP AX, BX  means  AX - BX

If AX = 5, BX = 3:
CMP AX, BX → 5 - 3 = 2 (positive)
JG label   → Jump (5 > 3 ✅)

If AX = 3, BX = 5:
CMP AX, BX → 3 - 5 = -2 (negative)
JL label   → Jump (3 < 5 ✅)
```

---

## 📊 BIG PICTURE: Branching Structure Taxonomy

```
┌────────────────────────────────────────────────────────────┐
│              BRANCHING STRUCTURES IN ASSEMBLY              │
└───────────────────────┬────────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
   ┌────▼────┐    ┌─────▼─────┐   ┌────▼────┐
   │IF-THEN  │    │IF-THEN-   │   │  CASE   │
   │         │    │   ELSE    │   │(SWITCH) │
   └────┬────┘    └─────┬─────┘   └────┬────┘
        │               │               │
   ┌────▼────┐    ┌─────▼─────┐   ┌────▼────┐
   │One path │    │Two paths  │   │Multiple │
   │Optional │    │Mandatory  │   │ paths   │
   └─────────┘    └───────────┘   └─────────┘
        │               │               │
   ┌────▼────┐    ┌─────▼─────┐   ┌────▼────┐
   │Execute  │    │Execute    │   │Execute  │
   │or Skip  │    │one of two │   │one of N │
   └─────────┘    └───────────┘   └─────────┘
```

---

## 🔷 Section 1: IF-THEN Structure

### **Concept:**
Execute a block of code **only if** a condition is true. Otherwise, **skip** it.

### **High-Level Pattern:**

```
IF condition is TRUE
THEN
    execute statements
END_IF
```

### **Flowchart:**

```
         ┌──────────────┐
         │  Condition?  │
         └───────┬──────┘
                 │
         ┌───────┴────────┐
         │                │
      ┌──▼──┐          ┌──▼──┐
      │TRUE │          │FALSE│
      └──┬──┘          └──┬──┘
         │                │
    ┌────▼─────┐          │
    │Execute   │          │
    │TRUE      │          │
    │Statements│          │
    └────┬─────┘          │
         │                │
         └────────┬───────┘
                  │
            ┌─────▼──────┐
            │  END_IF    │
            └────────────┘
```

### **Assembly Translation Pattern:**

```assembly
; IF condition is FALSE, jump over the TRUE block
    CMP operand1, operand2
    Jxx END_IF              ; Jxx = opposite of condition
    
    ; TRUE block statements here
    <statements>
    
END_IF:
    ; Continue program
```

### **Example 1: Absolute Value**

**Problem:** Replace AX with its absolute value (if negative, negate it)

**Pseudocode:**
```
IF AX < 0
THEN
    AX = -AX
END_IF
```

**Assembly Code:**

```assembly
        CMP AX, 0       ; Compare AX with 0
        JNL END_IF      ; Jump if Not Less (i.e., if AX >= 0)
        NEG AX          ; Make AX positive
END_IF:
        ; AX now contains absolute value
```

**Step-by-step Execution:**

```
Case 1: AX = 5 (positive)
┌─────────────────────────────────────┐
│ CMP AX, 0  → 5 - 0 = 5 (SF=0)      
│ JNL END_IF → 5 >= 0, so JUMP ✅     │
│ NEG AX     → SKIPPED               
│ Result: AX = 5                      
└─────────────────────────────────────┘

Case 2: AX = -5 (negative, stored as FFFBh)
┌─────────────────────────────────────┐
│ CMP AX, 0  → -5 - 0 = -5 (SF=1)    
│ JNL END_IF → -5 < 0, so NO JUMP ❌  
│ NEG AX     → EXECUTED               │
│ Result: AX = 5                      │
└─────────────────────────────────────┘
```

**Visual Execution Flow:**

```
AX = -5                     AX = 5
    │                          │
    ▼                          ▼
CMP AX, 0                  CMP AX, 0
    │                          │
    ▼                          ▼
AX < 0? YES               AX < 0? NO
    │                          │
    ▼                          │
NEG AX                         │
AX = 5                         │
    │                          │
    └──────────┬───────────────┘
               ▼
           END_IF
           AX = 5
```

---

## 🔶 Section 2: IF-THEN-ELSE Structure

### **Concept:**
Execute **one of two paths** based on a condition. Both paths eventually merge.

### **High-Level Pattern:**

```
IF condition is TRUE
THEN
    execute true-statements
ELSE
    execute false-statements
END_IF
```

### **Flowchart:**

```
         ┌──────────────┐
         │  Condition?  │
         └───────┬──────┘
                 │
         ┌───────┴────────┐
         │                │
      ┌──▼──┐          ┌──▼──┐
      │TRUE │          │FALSE│
      └──┬──┘          └──┬──┘
         │                │
    ┌────▼─────┐    ┌─────▼────┐
    │TRUE      │    │FALSE     │
    │Statements│    │Statements│
    └────┬─────┘    └─────┬────┘
         │                │
         └────────┬───────┘
                  │
            ┌─────▼──────┐
            │  END_IF    │
            └────────────┘
```

### **Assembly Translation Pattern:**

```assembly
    CMP operand1, operand2
    Jxx ELSE_              ; Jxx = opposite of desired condition
    
    ; TRUE block
    <true-statements>
    JMP END_IF             ; Skip ELSE block
    
ELSE_:
    ; FALSE block
    <false-statements>
    
END_IF:
    ; Continue program
```

### **Example 2: Display First Character**

**Problem:** Display whichever ASCII character (in AL or BL) comes first alphabetically

**Pseudocode:**
```
IF AL < BL
THEN
    Display AL
ELSE
    Display BL
END_IF
```

**Assembly Code:**

```assembly
        MOV AH, 2       ; DOS function: display character
        CMP AL, BL      ; Compare AL with BL
        JNBE ELSE_      ; Jump if Not Below or Equal (i.e., if AL > BL)
        
        ; TRUE block (AL <= BL)
        MOV DL, AL      ; Put AL in DL for display
        JMP DISPLAY     ; Skip ELSE block
        
ELSE_:  
        ; FALSE block (AL > BL)
        MOV DL, BL      ; Put BL in DL for display
        
DISPLAY:
        INT 21H         ; Display character in DL
END_IF:
        ; Continue program
```

**Example Execution:**

```
Case 1: AL = 'A' (41h), BL = 'Z' (5Ah)
┌──────────────────────────────────────────┐
│ CMP AL, BL → 41h - 5Ah (AL < BL)        
│ JNBE ELSE_ → 'A' <= 'Z', NO JUMP ❌      
│ MOV DL, AL → DL = 'A'                   │
│ JMP DISPLAY → Skip ELSE                 │
│ INT 21H    → Display 'A' ✅             
└──────────────────────────────────────────┘

Case 2: AL = 'Z' (5Ah), BL = 'A' (41h)
┌──────────────────────────────────────────┐
│ CMP AL, BL → 5Ah - 41h (AL > BL)        │
│ JNBE ELSE_ → 'Z' > 'A', JUMP ✅         
│ MOV DL, BL → DL = 'A'                   │
│ INT 21H    → Display 'A' ✅             
└──────────────────────────────────────────┘
```

**Visual Flow:**

```
AL='A', BL='Z'              AL='Z', BL='A'
      │                           │
      ▼                           ▼
  CMP AL,BL                   CMP AL,BL
      │                           │
      ▼                           ▼
   AL < BL? YES              AL < BL? NO
      │                           │
      ▼                           ▼
  MOV DL,AL                   ELSE_:
      │                       MOV DL,BL
      ▼                           │
  JMP DISPLAY                     │
      │                           │
      └───────────┬───────────────┘
                  ▼
              DISPLAY:
              INT 21H
              Outputs: 'A'
```

---

## 🔸 Section 3: CASE Structure (Multi-way Branch)

### **Concept:**
Choose **one of many paths** based on the value of an expression. Like a `switch` statement in C.

### **High-Level Pattern:**

```
CASE expression
    value_1: statements_1
    value_2: statements_2
    ...
    value_n: statements_n
END_CASE
```

### **Flowchart:**

```
         ┌──────────────┐
         │  Expression  │
         └───────┬──────┘
                 │
      ┌──────────┼──────────┐
      │          │          │
   ┌──▼──┐    ┌──▼──┐   ┌──▼──┐
   │Val 1│    │Val 2│   │Val N│
   └──┬──┘    └──┬──┘   └──┬──┘
      │          │          │
 ┌────▼───┐ ┌───▼────┐ ┌───▼────┐
 │Stmt 1  │ │Stmt 2  │ │Stmt N  │
 └────┬───┘ └───┬────┘ └───┬────┘
      │         │          │
      └─────────┼──────────┘
                │
          ┌─────▼──────┐
          │  END_CASE  │
          └────────────┘
```

### **Assembly Translation Pattern:**

```assembly
    CMP register, value
    JL  CASE_1          ; Test for first range
    JE  CASE_2          ; Test for exact value
    JG  CASE_3          ; Test for another range
    
CASE_1:
    <statements_1>
    JMP END_CASE
    
CASE_2:
    <statements_2>
    JMP END_CASE
    
CASE_3:
    <statements_3>
    ; Fall through to END_CASE
    
END_CASE:
```

### **Example 3: Sign Function**

**Problem:** Set BX based on sign of AX:
- If AX < 0 → BX = -1
- If AX = 0 → BX = 0
- If AX > 0 → BX = 1

**Pseudocode:**
```
CASE AX
    < 0: BX = -1
    = 0: BX = 0
    > 0: BX = 1
END_CASE
```

**Assembly Code:**

```assembly
        CMP AX, 0       ; Test AX against 0
        JL  NEG         ; If AX < 0, go to NEG
        JE  ZERO        ; If AX = 0, go to ZERO
        JG  POS         ; If AX > 0, go to POS
        
NEG:    MOV BX, -1      ; AX was negative
        JMP END_CASE
        
ZERO:   MOV BX, 0       ; AX was zero
        JMP END_CASE
        
POS:    MOV BX, 1       ; AX was positive
        ; No JMP needed (last case)
        
END_CASE:
        ; Continue program
```

**Important Note:** Only **ONE** `CMP` instruction is needed because **jump instructions don't modify flags**!

**Execution Examples:**

```
Case 1: AX = -5
┌────────────────────────────┐
│ CMP AX, 0  → SF=1, ZF=0   │
│ JL NEG     → JUMP ✅      
│ MOV BX, -1 → BX = FFFFh   │
│ JMP END_CASE              │
└────────────────────────────┘

Case 2: AX = 0
┌────────────────────────────┐
│ CMP AX, 0  → SF=0, ZF=1   │
│ JL NEG     → NO JUMP ❌   
│ JE ZERO    → JUMP ✅      
│ MOV BX, 0  → BX = 0       │
│ JMP END_CASE              │
└────────────────────────────┘

Case 3: AX = 5
┌────────────────────────────┐
│ CMP AX, 0  → SF=0, ZF=0   
│ JL NEG     → NO JUMP ❌   │
│ JE ZERO    → NO JUMP ❌   │
│ JG POS     → JUMP ✅      │
│ MOV BX, 1  → BX = 1       
└────────────────────────────┘
```

**Visual Decision Tree:**

```
         CMP AX, 0
             │
    ┌────────┼────────┐
    │        │        │
 ┌──▼─┐   ┌──▼─┐  ┌──▼─┐
 │AX<0│   │AX=0│  │AX>0│
 └──┬─┘   └──┬─┘  └──┬─┘
    │        │       │
 ┌──▼──┐ ┌──▼──┐ ┌──▼──┐
 │BX=-1│ │BX=0 │ │BX=1 │
 └──┬──┘ └──┬──┘ └──┬──┘
    │       │       │
    └───────┼───────┘
            │
       ┌────▼────┐
       │END_CASE │
       └─────────┘
```

---

## 🔗 Section 4: Compound Conditions (AND/OR)

### **AND Condition**

**Concept:** BOTH conditions must be true for the entire expression to be true.

```
Truth Table:
Cond1  Cond2  Result
FALSE  FALSE  FALSE
FALSE  TRUE   FALSE
TRUE   FALSE  FALSE
TRUE   TRUE   TRUE ✅
```

### **Short-Circuit AND Strategy:**

```
If Condition1 is FALSE → Skip immediately (no need to check Condition2)
If Condition1 is TRUE  → Check Condition2
```

### **Assembly Pattern:**

```assembly
    ; Check Condition1
    CMP operand1, value1
    Jxx EXIT            ; If Cond1 FALSE, exit
    
    ; Check Condition2
    CMP operand2, value2
    Jxx EXIT            ; If Cond2 FALSE, exit
    
    ; Both TRUE
    <statements>
    
EXIT:
```

### **Example 4: Uppercase Letter Check**

**Problem:** Read a character. If it's uppercase (A-Z), display it.

**Pseudocode:**
```
IF ('A' <= character) AND (character <= 'Z')
THEN
    Display character
END_IF
```

**Assembly Code:**

```assembly
        MOV AH, 1       ; DOS: read character
        INT 21H         ; Character now in AL
        MOV DL, AL      ; Save for display
        MOV AH, 2       ; DOS: display character
        
        CMP AL, 'A'     ; Is char >= 'A'?
        JL  END_IF      ; If less, skip display
        
        CMP AL, 'Z'     ; Is char <= 'Z'?
        JG  END_IF      ; If greater, skip display
        
        ; Both conditions TRUE
        INT 21H         ; Display character
        
END_IF:
```

**Execution Examples:**

```
Case 1: Input = 'M' (4Dh)
┌───────────────────────────────┐
│ CMP AL, 'A' → 'M' >= 'A' ✅   │
│ JL END_IF   → NO JUMP         
│ CMP AL, 'Z' → 'M' <= 'Z' ✅   │
│ JG END_IF   → NO JUMP         
│ INT 21H     → Display 'M' ✅  │
└───────────────────────────────┘

Case 2: Input = '5' (35h)
┌───────────────────────────────┐
│ CMP AL, 'A' → '5' < 'A' ❌    
│ JL END_IF   → JUMP ✅         
│ (Skipped)   → No display      
└───────────────────────────────┘

Case 3: Input = 'z' (7Ah)
┌───────────────────────────────┐
│ CMP AL, 'A' → 'z' >= 'A' ✅   
│ JL END_IF   → NO JUMP         
│ CMP AL, 'Z' → 'z' > 'Z' ❌    │
│ JG END_IF   → JUMP ✅         
│ (Skipped)   → No display      
└───────────────────────────────┘
```

**Visual Flow:**

```
Input: 'M'                 Input: '5'
    │                          │
    ▼                          ▼
AL >= 'A'? YES            AL >= 'A'? NO
    │                          │
    ▼                          ▼
AL <= 'Z'? YES            JL END_IF ✅
    │                          │
    ▼                          │
Display 'M' ✅                
    │                          │
    └──────────┬───────────────┘
               ▼
           END_IF
```

---

### **OR Condition**

**Concept:** At least ONE condition must be true for the entire expression to be true.

```
Truth Table:
Cond1  Cond2  Result
FALSE  FALSE  FALSE
FALSE  TRUE   TRUE ✅
TRUE   FALSE  TRUE ✅
TRUE   TRUE   TRUE ✅
```

### **Short-Circuit OR Strategy:**

```
If Condition1 is TRUE → Execute immediately (no need to check Condition2)
If Condition1 is FALSE → Check Condition2
```

### **Assembly Pattern:**

```assembly
    ; Check Condition1
    CMP operand1, value1
    Jxx THEN            ; If Cond1 TRUE, go to THEN
    
    ; Check Condition2
    CMP operand2, value2
    Jxx THEN            ; If Cond2 TRUE, go to THEN
    
    ; Both FALSE
    JMP ELSE_
    
THEN:
    <true-statements>
    JMP END_IF
    
ELSE_:
    <false-statements>
    
END_IF:
```

### **Example 5: Accept 'y' or 'Y'**

**Problem:** Read a character. If it's 'y' or 'Y', display it; otherwise terminate.

**Pseudocode:**
```
IF (char = 'y') OR (char = 'Y')
THEN
    Display character
ELSE
    Terminate
END_IF
```

**Assembly Code:**

```assembly
        MOV AH, 1       ; DOS: read character
        INT 21H         ; Character in AL
        
        CMP AL, 'y'     ; Is it lowercase 'y'?
        JE  THEN        ; If yes, display
        
        CMP AL, 'Y'     ; Is it uppercase 'Y'?
        JE  THEN        ; If yes, display
        
        JMP ELSE_       ; Neither 'y' nor 'Y'
        
THEN:
        MOV AH, 2       ; DOS: display character
        MOV DL, AL
        INT 21H
        JMP END_IF
        
ELSE_:
        ; Terminate program
        MOV AH, 4CH
        INT 21H
        
END_IF:
```

**Execution Examples:**

```
Case 1: Input = 'y'
┌───────────────────────────────┐
│ CMP AL, 'y' → Match ✅       │
│ JE THEN     → JUMP ✅        │
│ Display 'y' ✅               │
└───────────────────────────────┘

Case 2: Input = 'Y'
┌───────────────────────────────┐
│ CMP AL, 'y' → No match ❌     
│ JE THEN     → NO JUMP         
│ CMP AL, 'Y' → Match ✅        │
│ JE THEN     → JUMP ✅         │
│ Display 'Y' ✅                
└───────────────────────────────┘

Case 3: Input = 'n'
┌───────────────────────────────┐
│ CMP AL, 'y' → No match ❌    
│ JE THEN     → NO JUMP         │
│ CMP AL, 'Y' → No match ❌     
│ JE THEN     → NO JUMP         │
│ JMP ELSE_   → JUMP ✅         
│ Terminate   ✅                
└───────────────────────────────┘
```

**Visual Flow:**

```
     Input
       │
   ┌───▼───┐
   │AL='y'?│
   └───┬───┘
       │
   ┌───┴───┐
   │YES│NO │
   │   │   │
   │   ▼   │
   │  AL='Y'?
   │   │   │
   │ ┌─┴─┐ │
   │ │YES│NO
   │ │   │ │
   ▼ ▼   │ ▼
  ┌───────┐ ┌─────────┐
  │Display│ │Terminate│
  └───────┘ └─────────┘
```

---

## 🎨 Complete Comparison: All Three Structures

```
┌─────────────────────────────────────────────────────────────┐
│                   STRUCTURE COMPARISON                      │
├─────────────┬─────────────────┬─────────────────────────────┤
│ IF-THEN     │ IF-THEN-ELSE    │ CASE                        │
├─────────────┼─────────────────┼─────────────────────────────┤
│   Cond      │    Cond         │      Expr                   │
│    │        │     │           │       │                     │
│  ┌─┴─┐      │   ┌─┴─┐         │  ┌────┼────┐                │
│  │YES│      │   │YES│NO       │  │    │    │                │
│  │   │      │   │   │ │       │ V1   V2   V3                │
│  ▼   │      │   ▼   ▼         │  │    │    │                │
│ True │      │ True False      │  ▼    ▼    ▼                │
│ Block│      │ Block Block     │ S1   S2   S3                │
│  │   │      │   │   │         │  │    │    │                │
│  └───┘      │   └───┴─┐       │  └────┴────┘                │
│             │         │       │                             │
│  1 Path     │   2 Paths       │  N Paths                    │
│  Optional   │   Mandatory     │  One selected               │
└─────────────┴─────────────────┴─────────────────────────────┘
```

---

## 📝 Code Pattern Summary

### **IF-THEN Template:**
```assembly
    CMP reg, value
    Jopposite END_IF    ; Use opposite of desired condition
    <true-statements>
END_IF:
```

### **IF-THEN-ELSE Template:**
```assembly
    CMP reg, value
    Jopposite ELSE_
    <true-statements>
    JMP END_IF
ELSE_:
    <false-statements>
END_IF:
```

### **CASE Template:**
```assembly
    CMP reg, value
    JL  CASE_1
    JE  CASE_2
    JG  CASE_3
CASE_1:
    <statements_1>
    JMP END_CASE
CASE_2:
    <statements_2>
    JMP END_CASE
CASE_3:
    <statements_3>
END_CASE:
```

### **AND Template:**
```assembly
    CMP reg1, value1
    Jfail EXIT
    CMP reg2, value2
    Jfail EXIT
    <both-true-statements>
EXIT:
```

### **OR Template:**
```assembly
    CMP reg, value1
    Jsuccess THEN
    CMP reg, value2
    Jsuccess THEN
    JMP ELSE_
THEN:
    <true-statements>
    JMP END_IF
ELSE_:
    <false-statements>
END_IF:
```

---

## 🎯 Quick Reference Cheat Sheet

```
┌──────────────────────────────────────────────────────────────┐
│              BRANCHING STRUCTURES CHEAT SHEET                │
├──────────────────────────────────────────────────────────────┤
│ IF-THEN                                                      │
│  • One optional path                                         │
│  • Use opposite jump to skip                                 │
│  • Pattern: Jopposite END_IF                                 │
├──────────────────────────────────────────────────────────────┤
│ IF-THEN-ELSE                                                 │
│  • Two mandatory paths                                       │
│  • TRUE path needs JMP to skip FALSE                         │
│  • Pattern: Jopposite ELSE_ ... JMP END_IF                   │
├──────────────────────────────────────────────────────────────┤
│ CASE                                                         │
│  • Multiple paths                                            │
│  • One CMP, multiple jumps                                   │
│  • Each case needs JMP END_CASE (except last)                │
├──────────────────────────────────────────────────────────────┤
│ AND Conditions                                               │
│  • Both must be TRUE                                         │
│  • Short-circuit: exit on first FALSE                        │
│  • Pattern: Two CMPs, both jump to EXIT if fail              │
├──────────────────────────────────────────────────────────────┤
│ OR Conditions                                                │
│  • At least one must be TRUE                                 │
│  • Short-circuit: execute on first TRUE                      │
│  • Pattern: Two CMPs, both jump to THEN if succeed           │
└──────────────────────────────────────────────────────────────┘
```

---

## ✅ Practice Problems

### **Problem 1:**
Write IF-THEN to make BX = 0 if AX is even.

<details>
<summary>Solution</summary>

```assembly
    TEST AX, 1      ; Check if bit 0 is set
    JNZ END_IF      ; If odd (bit 0 = 1), skip
    MOV BX, 0       ; Make BX = 0
END_IF:
```
</details>

### **Problem 2:**
Write IF-THEN-ELSE: if CX > 10, set DX = 1; else set DX = 2.

<details>
<summary>Solution</summary>

```assembly
    CMP CX, 10
    JLE ELSE_
    MOV DX, 1
    JMP END_IF
ELSE_:
    MOV DX, 2
END_IF:
```
</details>

### **Problem 3:**
Write CASE: if AL = 1 → BL = 'A', if AL = 2 → BL = 'B', if AL = 3 → BL = 'C'.

<details>
<summary>Solution</summary>

```assembly
    CMP AL, 1
    JE CASE_1
    CMP AL, 2
    JE CASE_2
    CMP AL, 3
    JE CASE_3
    JMP END_CASE
CASE_1:
    MOV BL, 'A'
    JMP END_CASE
CASE_2:
    MOV BL, 'B'
    JMP END_CASE
CASE_3:
    MOV BL, 'C'
END_CASE:
```
</details>

### **Problem 4:**
Write AND: if (AX > 0) AND (AX < 100), set BX = 1.

<details>
<summary>Solution</summary>

```assembly
    CMP AX, 0
    JLE END_IF
    CMP AX, 100
    JGE END_IF
    MOV BX, 1
END_IF:
```
</details>

### **Problem 5:**
Write OR: if (AL = 'a') OR (AL = 'A'), display it.

<details>
<summary>Solution</summary>

```assembly
    CMP AL, 'a'
    JE DISPLAY
    CMP AL, 'A'
    JNE END_IF
DISPLAY:
    MOV AH, 2
    MOV DL, AL
    INT 21H
END_IF:
```
</details>

---

## 🚀 Exam Tips

1. **Jump Direction Trick:**
   - To execute block when condition TRUE → use **opposite** jump to skip
   - Example: Want to execute when AX > 0? Use `JLE END_IF` (skip if ≤ 0)

2. **Don't Forget JMP:**
   - In IF-THEN-ELSE: TRUE block needs `JMP END_IF`
   - In CASE: Each case needs `JMP END_CASE` (except last)

3. **Flags Persist:**
   - One CMP can serve multiple jumps
   - Jumps don't modify flags!

4. **AND = Multiple Exits:**
   - Each condition can jump to END_IF

5. **OR = Multiple Entries:**
   - Each condition can jump to THEN

6. **Common Mistakes:**
   - Forgetting `JMP END_IF` in ELSE
   - Using wrong jump direction
   - Re-comparing in CASE (only need one CMP!)

---

**Good luck on your exam! 🎓 Master these patterns and you'll ace it!**
