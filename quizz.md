---
# COMP6062001 — Compilation Techniques

## **QUIZ 3 (FINAL QUIZ)**

### **Topic:** Table-Driven Parsing (LL & LR)

### **Duration:** 100 minutes

### **Format:** Individual, open-computer, coding work
---

## **General Instructions**

Choose **ONE** grammar only.

You are given **two Python files**:

- `ll1_parser_template.py`
- `lr_parser_template.py`

Each contains a parser skeleton.
You **must not** modify the core parser logic.
You only fill in the grammar-specific data structures.

Input is already tokenized (list of tokens).
Your parser must implement:

```
def parse_ll1(tokens: list[str]) -> str     # returns "ACCEPT" or "ERROR"
def parse_lr(tokens: list[str]) -> str      # returns "ACCEPT" or "ERROR"
```

You may also implement your own full parser without using the skeleton.

### **Submission**

Submit one of:

- Completed `ll1_parser_template.py` **OR**
- Completed `lr_parser_template.py`

Also submit your written FIRST/FOLLOW or LR item sets + parsing tables (paper or file).

Tree/AST is optional.

---

# OPTION A — LL(1) Predictive Parsing (50 minutes)

### **Task 1 — FIRST/FOLLOW**

Compute:

- FIRST sets
- FOLLOW sets
- LL(1) parsing table using FIRST/FOLLOW

You may write this on paper or in a text file.

---

### **Task 2 — Fill the LL(1) Table in Code**

In `ll1_parser_template.py`, fill:

```
START_SYMBOL
NONTERMINALS
TERMINALS
PARSE_TABLE = {
    NONTERM: { lookahead: RHS_list }
}
```

Use `['ε']` for epsilon.

---

### **Task 3 — Test Your LL(1) Parser**

Test on:

- **Legitimate input** → expect `"ACCEPT"`
- **Illegitimate input** → expect `"ERROR"`

Tokens are space-separated; append `$` as end marker.

---

# OPTION B — SLR(1) Bottom-Up Parsing (50 minutes)

### **Task 1 — LR(0) Automata + SLR(1) Table**

Steps:

1. Augment grammar: `S' → S`
2. Construct LR(0) item sets
3. Build **ACTION** and **GOTO** tables
4. Use FOLLOW sets to place **reduce** actions (SLR method)

Submit written LR automata + tables.

---

### **Task 2 — Fill LR Tables in Code**

In `lr_parser_template.py`, fill:

```
PRODUCTIONS = [
    (LHS, [RHS symbols])
]

ACTION = {
    state: {
        terminal: ('shift', s) | ('reduce', i) | ('accept',)
    }
}

GOTO = {
    state: { nonterminal: next_state }
}
```

Index productions starting from 0.

---

### **Task 3 — Test Your LR Parser**

Test on:

- **Legitimate input** → `"ACCEPT"`
- **Illegitimate input** → `"ERROR"`

---

# Grammar Allocation (Your Grammar)

You (Riki Awal Syahputra – **2802471404**) use:

### **GRAMMAR 8**

You choose between:

## **GRAMMAR 8A**

```
E → T R
R → + T R | ε
T → - T | i
```

Terminals: `i`, `+`, `-`
Legitimate: `- i + i`
Illegitimate: `+ - i`

## **GRAMMAR 8B**

```
E → E + T
E → T
T → i
```

Terminals: `i`, `+`
Legitimate: `i + i + i`
Illegitimate: `+ i i`

---

# Complete Grammar List (All Students)

(Exactly as provided in the original file — omitted here for brevity to keep the README clean. All 10 grammar pairs remain the same.)

---

# Appendix — LL(1) Parser Template (Python)

```python
# ll1_parser_template.py
# ===========================
# LL(1) TABLE-DRIVEN PARSER
# ===========================

START_SYMBOL = 'E'       # TODO: set correctly for the given grammar
NONTERMINALS = {'E', 'R', 'T'}   # TODO: adjust if needed
TERMINALS = {'i', '+'}           # TODO: adjust if needed

# PARSE_TABLE[NONTERM][lookahead] = RHS list
PARSE_TABLE = {
    # TODO: fill using LL(1) table
}

def parse_ll1(tokens: list[str], verbose: bool = False) -> str:
    ...
```

---

# Appendix — LR Parser Template (Python)

```python
# lr_parser_template.py
# ===========================
# LR TABLE-DRIVEN PARSER
# ===========================

PRODUCTIONS = []      # fill this
ACTION = {}           # fill this
GOTO = {}             # fill this

def parse_lr(tokens: list[str], verbose: bool = False) -> str:
    ...
```

---

# End of README
