# COMP6062001 - Compilation Techniques
## Quiz 3 (Final Quiz) - Table-Driven Parsing

**Student:** Riki Awal Syahputra  
**Student ID:** 2802471404  
**Attendance Number:** 22  
**Grammar:** Grammar 8B  
**Parsing Method:** SLR(1) Bottom-Up Parsing

---

## Grammar Specification

**Grammar 8B:**
```
E → E + T
E → T
T → i
```

**Terminals:** `i`, `+`  
**Nonterminals:** `E`, `T`  
**Start Symbol:** `E`

---

## Project Structure

```
.
├── lr_parser_template.ipynb    # SLR(1) parser implementation (Jupyter Notebook)
├── grammar_8b_analysis.md      # Written analysis (LR automaton and parsing tables)
└── README.md                   # This file
```

---

## Implementation Details

### Augmented Grammar

```
0: E' → E
1: E → E + T
2: E → T
3: T → i
```

### Parser Specifications

- **Type:** SLR(1) Table-Driven Parser
- **States:** 7 LR(0) item sets
- **Implementation:** Python 3
- **Input Format:** Space-separated tokens ending with `$`
- **Output:** `"ACCEPT"` or `"ERROR"`

### Function Signature

```python
def parse_lr(tokens: list[str], verbose: bool = False) -> str
```

---

## Test Cases

### Required Test Cases

1. **Legitimate Input:** `i + i + i`
   - Expected: ACCEPT
   - Status: PASS

2. **Illegitimate Input:** `+ i i`
   - Expected: ERROR
   - Status: PASS

### Additional Test Cases

3. **Single Identifier:** `i`
   - Expected: ACCEPT
   - Status: PASS

4. **Incomplete Expression:** `i +`
   - Expected: ERROR
   - Status: PASS

---

## Usage

### Running the Parser

Open `lr_parser_template.ipynb` in Jupyter Notebook or JupyterLab and execute all cells sequentially.

Alternatively, use the command line:
```bash
jupyter notebook lr_parser_template.ipynb
```

### Custom Input

To test custom input, add a new cell with:
```python
tokens = ['your', 'tokens', 'here', '$']
result = parse_lr(tokens, verbose=True)
print(f"Result: {result}")
```

---

## Documentation

Complete written analysis including LR(0) item sets, FOLLOW sets, ACTION table, and GOTO table can be found in `grammar_8b_analysis.md`.

---

## Submission Contents

1. `lr_parser_template.ipynb` - Complete SLR(1) parser implementation
2. `grammar_8b_analysis.md` - Written work showing:
   - LR(0) automaton construction
   - FOLLOW sets computation
   - ACTION and GOTO tables
   - Parsing traces for test cases

---

## Notes

This implementation uses a table-driven approach where the core parser logic remains unchanged. Only the grammar-specific data structures (PRODUCTIONS, ACTION, GOTO) are filled according to Grammar 8B specifications.

The grammar contains left recursion (`E → E + T`), which makes it unsuitable for LL(1) parsing but appropriate for bottom-up LR parsing methods.

