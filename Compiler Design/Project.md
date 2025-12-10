# Simple Project Working Flow Explanation

## 🎯 **Big Picture: What Does This Compiler Do?**

```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐      ┌──────────┐
│ Source Code │  →   │  Our Compiler│   →  │   Execute   │  →   │  Output  │
│  (test.prog)│      │   (main.exe) │      │   Program   │      │ (Results)│
└─────────────┘      └──────────────┘      └─────────────┘      └──────────┘
```

**In one sentence:** Our compiler reads a program file, analyzes it, and executes it.

---

## 📁 **Project Files & Their Jobs**

```
┌─────────────────────────────────────────────────────────────────┐
│                      PROJECT FILES                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. main.c          → Boss (coordinates everything)             │
│                                                                 │
│  2. lexer.l         → Word Identifier (finds tokens)            │
│     ↓ (generates)                                               │
│     lex.yy.c        → Generated lexer code                      │
│                                                                 │
│  3. parser.y        → Grammar Checker (builds tree)             │
│     ↓ (generates)                                               │
│     parser.tab.c    → Generated parser code                     │
│     parser.tab.h    → Token definitions                         │
│                                                                 │
│  4. ast.h / ast.c   → Tree Builder & Executor                   │
│                                                                 │
│  5. types.h         → Type Definitions                          │
│                                                                 │
│  6. semantic.c      → Rule Checker (validates code)             │
│                                                                 │
│  7. codegen.c       → Code Generator (if needed)                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 **Step-by-Step Working Flow**

### **PHASE 1: User Runs the Program**

```bash
./compiler test.prog
```

**What happens:**
- Operating system starts main.c
- `main()` function begins execution

---

### **PHASE 2: main.c Takes Control**

```c
int main(int argc, char **argv) {
    // Step 1: Check if user provided a file
    if (argc != 2) {
        // Error: No file provided
    }
    
    // Step 2: Open the file
    FILE *f = fopen(argv[1], "r");
    
    // Step 3: Connect file to lexer
    yyin = f;
    
    // Step 4: Start compilation
    yyparse();
    
    // Step 5: Execute program
    eval(root);
    
    // Step 6: Cleanup
    fclose(f);
}
```

**Think of main.c as a BOSS who:**
1. Checks if everything is ready
2. Opens the file
3. Calls workers (lexer, parser)
4. Executes the result
5. Cleans up

---

### **PHASE 3: Lexer Reads and Tokenizes** (lexer.l → lex.yy.c)

```
Input File: test.prog
─────────────────────
int x = 10;
float y = 5.5;
x = x + y;

                ↓ (Lexer reads character by character)

Token Stream:
─────────────────────
[INT] [ID:"x"] [=] [NUMBER:10] [;]
[FLOAT] [ID:"y"] [=] [NUMBER:5.5] [;]
[ID:"x"] [=] [ID:"x"] [+] [ID:"y"] [;]
```

**Think of lexer as a WORD IDENTIFIER who:**
- Reads text character by character
- Groups characters into meaningful words (tokens)
- Labels each word (INT, FLOAT, NUMBER, ID, etc.)
- Sends tokens to parser

**Real-World Analogy:**
```
Like reading a sentence and identifying:
"The cat sat on the mat"
↓
[Article:"The"] [Noun:"cat"] [Verb:"sat"] [Preposition:"on"] [Article:"the"] [Noun:"mat"]
```

---

### **PHASE 4: Parser Checks Grammar & Builds Tree** (parser.y → parser.tab.c)

```
Token Stream:              
─────────────────────
[INT] [ID:"x"] [=] [NUMBER:10] [;]

                ↓ (Parser checks grammar rules)

Does this follow grammar?
✓ declaration → type identifier = expression ;
✓ type → INT
✓ identifier → "x"
✓ expression → NUMBER(10)
✓ Valid!

                ↓ (Parser builds Abstract Syntax Tree)

        DECLARATION
            │
    ┌───────┼───────┐
  INT      "x"    NUMBER
                    │
                   10
```

**Think of parser as a GRAMMAR TEACHER who:**
- Takes tokens from lexer
- Checks if they follow language rules
- If correct: Builds a tree structure (AST)
- If wrong: Reports syntax error
- Stores tree in `root` variable

**Real-World Analogy:**
```
Sentence: "The cat sat on mat"
                              ↑ Missing "the"
Grammar Teacher: ❌ Error! Article missing before "mat"

Sentence: "The cat sat on the mat"
Grammar Teacher: ✓ Correct! Builds sentence diagram.
```

---

### **PHASE 5: AST Stores Program Structure** (ast.h / ast.c)

```
Complete Program Tree:

                    PROGRAM (root)
                        │
        ┌───────────────┼───────────────┐
        │               │               │
   DECLARATION    DECLARATION      ASSIGNMENT
        │               │               │
    ┌───┴───┐      ┌───┴───┐      ┌────┴────┐
  INT  "x"  10   FLOAT "y" 5.5   "x"    BINARY_OP(+)
                                         │
                                    ┌────┴────┐
                                   "x"       "y"
```

**Think of AST as a FAMILY TREE that:**
- Organizes the entire program
- Shows relationships between parts
- Can be traversed (walked through)
- Stores in `root` variable (the top of tree)

**Real-World Analogy:**
```
Like a family tree:
         Grandparent
             │
    ┌────────┼────────┐
  Parent1  Parent2  Parent3
    │         │        │
  Child1   Child2    Child3
```

---

### **PHASE 6: Semantic Checker Validates** (semantic.c)

```
Symbol Table:
┌──────────┬──────┬────────┐
│   Name   │ Type │ Value  │
├──────────┼──────┼────────┤
│    x     │ int  │   10   │
│    y     │ float│  5.5   │
└──────────┴──────┴────────┘

Checks:
✓ Is 'x' declared? Yes
✓ Is 'y' declared? Yes
✓ Can we do 'x + y'? Yes (int + float = valid)
✓ Are types compatible? Yes
```

**Think of semantic checker as a RULE VALIDATOR who:**
- Maintains a symbol table (list of variables)
- Checks if variables are declared before use
- Verifies type compatibility
- Ensures operations make sense

**Real-World Analogy:**
```
Chef checking ingredients:
✓ Do we have flour? Yes
✓ Do we have eggs? Yes
✓ Can we mix flour + eggs? Yes
✗ Can we mix flour + nails? No! Type error!
```

---

### **PHASE 7: Execute the Program** (eval() in ast.c)

```c
eval(root);  // Called from main.c
```

**What eval() does:**

```
Traverse Tree:
──────────────

1. Visit DECLARATION (int x = 10)
   → Store: x = 10

2. Visit DECLARATION (float y = 5.5)
   → Store: y = 5.5

3. Visit ASSIGNMENT (x = x + y)
   → Read: x = 10
   → Read: y = 5.5
   → Calculate: 10 + 5.5 = 15.5
   → Store: x = 15.5

4. Print Results
   → x = 15.5
   → y = 5.5
```

**Think of eval() as a RUNNER who:**
- Walks through the tree
- Executes each instruction
- Stores values in memory
- Performs calculations
- Prints output

**Real-World Analogy:**
```
Following a recipe step-by-step:
1. Take 2 eggs → Done
2. Add 1 cup flour → Done
3. Mix together → Done
4. Bake for 30 mins → Done
```

---

## 🎬 **Complete Flow Animation**

```
USER TYPES:
──────────────────────────────────────────────────────────────
./compiler test.prog


STEP 1: main.c Opens File
──────────────────────────────────────────────────────────────
main() {
    FILE *f = fopen("test.prog", "r");  ✓ Opened
}


STEP 2: main.c Connects to Lexer
──────────────────────────────────────────────────────────────
    yyin = f;  ← Lexer now reads from test.prog


STEP 3: main.c Calls Parser
──────────────────────────────────────────────────────────────
    yyparse();  ← Start compilation
        │
        ├─→ Parser: "I need tokens!"
        │       │
        │       └─→ Lexer: "Here are tokens!"
        │               │
        │               └─→ Reads: "int x = 10;"
        │                   Returns: [INT][ID][=][NUMBER][;]
        │
        ├─→ Parser: "Building tree..."
        │       │
        │       └─→ Creates AST nodes
        │           Stores in 'root'
        │
        └─→ Parser: "Done! Tree ready."


STEP 4: main.c Checks Success
──────────────────────────────────────────────────────────────
    if (yyparse() == 0 && root) {  ✓ Success!


STEP 5: main.c Prints Header
──────────────────────────────────────────────────────────────
    printf("========== Mini Compiler Execution ==========");
    printf("File: test.prog");
    printf("Time: Mon Dec 9 14:30:45 2025");
    printf("--------------------------------------------");


STEP 6: main.c Executes Program
──────────────────────────────────────────────────────────────
    eval(root);  ← Execute the AST
        │
        ├─→ Visits DECLARATION(x)
        │   Stores: x = 10
        │
        ├─→ Visits DECLARATION(y)
        │   Stores: y = 5.5
        │
        ├─→ Visits ASSIGNMENT(x = x + y)
        │   Calculates: 10 + 5.5 = 15.5
        │   Stores: x = 15.5
        │
        └─→ Prints: 
            x = 15.5
            y = 5.5


STEP 7: main.c Prints Footer & Cleanup
──────────────────────────────────────────────────────────────
    printf("============================================");
    fclose(f);  ← Close file
    return 0;   ← Exit successfully
```

---

## 🤝 **How Files Collaborate**

```
┌─────────────────────────────────────────────────────────────┐
│                    FILE COLLABORATION                        │
└─────────────────────────────────────────────────────────────┘

main.c (BOSS)
    │
    │ "Open file"
    ├──→ Opens test.prog
    │
    │ "Connect to lexer"
    ├──→ Sets yyin = file pointer
    │
    │ "Start parsing"
    ├──→ Calls yyparse()
    │           │
    │           │ (Parser from parser.tab.c)
    │           │
    │           ├──→ "Give me tokens!"
    │           │        │
    │           │        └──→ Calls yylex()
    │           │                    │
    │           │                    │ (Lexer from lex.yy.c)
    │           │                    │
    │           │                    ├──→ Reads from yyin
    │           │                    ├──→ Matches patterns
    │           │                    ├──→ Returns token
    │           │                    │
    │           │        ┌───────────┘
    │           │        │
    │           ├──→ Receives token
    │           ├──→ Checks grammar
    │           ├──→ Calls AST functions:
    │           │        │
    │           │        ├──→ createNumberNode()
    │           │        ├──→ createBinaryOp()
    │           │        └──→ createDeclaration()
    │           │                    │
    │           │                    │ (From ast.c)
    │           │                    │
    │           │                    ├──→ Allocates memory
    │           │                    ├──→ Fills node data
    │           │                    └──→ Returns node pointer
    │           │
    │           └──→ Stores final tree in 'root'
    │
    │ "Execute program"
    └──→ Calls eval(root)
                │
                │ (From ast.c)
                │
                ├──→ Traverses tree
                ├──→ Executes statements
                ├──→ Evaluates expressions
                └──→ Prints output
```

---

## 💡 **Key Concepts for Teacher**

### **1. Two-Phase Process**

```
PHASE 1: Analysis (Understanding the code)
─────────────────────────────────────────
Lexer   → Tokenization
Parser  → Syntax checking
AST     → Structure building
Semantic→ Rule validation

PHASE 2: Execution (Running the code)
─────────────────────────────────────────
eval()  → Tree traversal
        → Statement execution
        → Output generation
```

### **2. Why Use a Tree?**

```
Without Tree (Linear):        With Tree (Structured):
─────────────────────         ─────────────────────
Execute line 1                      PROGRAM
Execute line 2                          │
Execute line 3                  ┌───────┼───────┐
...                           stmt1   stmt2   stmt3
                                 │
Hard to handle:               Can handle:
- Nested structures           - Nested if/for
- Expressions                 - Complex expressions
- Scope                       - Variable scope
```

### **3. Why Separate Lexer and Parser?**

```
Separation of Concerns:
───────────────────────

Lexer  → "What are the words?"
         (Low-level: characters → tokens)

Parser → "What's the meaning?"
         (High-level: tokens → structure)

Like reading a book:
Step 1: Recognize words (lexer)
Step 2: Understand sentences (parser)
```

---

## 🎤 **Simple Explanation for Teacher**

### **Version 1: Super Simple**

"Our compiler works in a pipeline:

1. **main.c** opens the source file
2. **Lexer** breaks it into words (tokens)
3. **Parser** checks grammar and builds a tree
4. **AST** stores the program structure
5. **eval()** walks the tree and executes it
6. **main.c** prints results and cleans up

It's like reading a recipe: First identify ingredients (lexer), then understand steps (parser), then cook (execute)."

### **Version 2: Technical**

"The project follows the classic compiler architecture:

**main.c** is the orchestrator that:
- Opens the input file
- Connects it to the lexer via `yyin`
- Invokes `yyparse()` to start compilation

**Lexical Analysis (lexer.l):**
- Scans characters and produces tokens
- Uses regular expressions for pattern matching
- Returns token codes to parser

**Syntax Analysis (parser.y):**
- Receives tokens from lexer
- Validates against grammar rules
- Constructs Abstract Syntax Tree using ast.c functions
- Stores result in global `root` variable

**Execution (ast.c):**
- `eval()` recursively traverses the AST
- Executes statements in order
- Evaluates expressions
- Manages variable storage
- Produces output

The key insight is separation of concerns: each phase has a specific responsibility, and they collaborate through well-defined interfaces (`yyin`, `root`, function calls)."

---

## ✅ **Summary Diagram**

```
┌──────────────────────────────────────────────────────────────┐
│                    PROJECT WORKFLOW                          │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  INPUT: test.prog                                            │
│    │                                                         │
│    ├─→ main.c opens file                                     │
│    │                                                         │
│    ├─→ Lexer (lex.yy.c) tokenizes                            │
│    │   Output: [INT][ID][=][NUMBER][;]...                    │
│    │                                                         │
│    ├─→ Parser (parser.tab.c) validates & builds tree         │
│    │   Output: AST stored in 'root'                          │
│    │                                                         │
│    ├─→ Semantic (semantic.c) validates rules                 │
│    │   Output: Validated AST                                 │
│    │                                                         │
│    ├─→ eval(root) executes program                           │
│    │   Output: Results printed to screen                     │
│    │                                                         │
│    └─→ main.c cleans up and exits                            │
│                                                              │
│  OUTPUT: Program results                                     │
└──────────────────────────────────────────────────────────────┘
```

**This is the complete working flow! You can now explain it confidently! 🚀**
