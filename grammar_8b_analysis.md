# Grammar 8B - SLR(1) Parser Analysis
**Student:** Riki Awal Syahputra (2802471404)  
**Attendance Number:** 22  
**Quiz:** COMP6062001 - Quiz 3 (Final Quiz)

---

## Grammar 8B

```
E → E + T
E → T
T → i
```

**Terminals:** `i`, `+`  
**Nonterminals:** `E`, `T`  
**Start Symbol:** `E`

---

## Augmented Grammar

```
0: E' → E
1: E → E + T
2: E → T
3: T → i
```

---

## LR(0) Item Sets (Automaton)

### State 0 (Initial State)
```
E' → •E
E → •E + T
E → •T
T → •i
```
**Transitions:**
- On `E` → State 1
- On `T` → State 2
- On `i` → State 3

### State 1
```
E' → E•
E → E• + T
```
**Transitions:**
- On `+` → State 4

### State 2
```
E → T•
```
**No transitions** (reduce state)

### State 3
```
T → i•
```
**No transitions** (reduce state)

### State 4
```
E → E +• T
T → •i
```
**Transitions:**
- On `T` → State 5
- On `i` → State 6

### State 5
```
E → E + T•
```
**No transitions** (reduce state)

### State 6
```
T → i•
```
**No transitions** (reduce state)

---

## FOLLOW Sets (for SLR(1))

- **FOLLOW(E')** = `{$}`
- **FOLLOW(E)** = `{$, +}`
- **FOLLOW(T)** = `{$, +}`

---

## SLR(1) Parsing Tables

### ACTION Table

| State | i    | +    | $      |
|-------|------|------|--------|
| 0     | s3   | —    | —      |
| 1     | —    | s4   | accept |
| 2     | —    | r2   | r2     |
| 3     | —    | r3   | r3     |
| 4     | s6   | —    | —      |
| 5     | —    | r1   | r1     |
| 6     | —    | r3   | r3     |

**Legend:**
- `sN` = shift and push state N
- `rN` = reduce by production N
- `accept` = accept input
- `—` = error

### GOTO Table

| State | E | T |
|-------|---|---|
| 0     | 1 | 2 |
| 1     | — | — |
| 2     | — | — |
| 3     | — | — |
| 4     | — | 5 |
| 5     | — | — |
| 6     | — | — |

---

## Test Cases

### Test 1: Legitimate Input `i + i + i`

**Expected:** ACCEPT ✓

**Parsing Trace:**

| Step | Stack      | Input       | Action              |
|------|------------|-------------|---------------------|
| 0    | 0          | i + i + i $ | shift 3             |
| 1    | 0 3        | + i + i $   | reduce by 3: T → i  |
| 2    | 0 2        | + i + i $   | reduce by 2: E → T  |
| 3    | 0 1        | + i + i $   | shift 4             |
| 4    | 0 1 4      | i + i $     | shift 6             |
| 5    | 0 1 4 6    | + i $       | reduce by 3: T → i  |
| 6    | 0 1 4 5    | + i $       | reduce by 1: E → E + T |
| 7    | 0 1        | + i $       | shift 4             |
| 8    | 0 1 4      | i $         | shift 6             |
| 9    | 0 1 4 6    | $           | reduce by 3: T → i  |
| 10   | 0 1 4 5    | $           | reduce by 1: E → E + T |
| 11   | 0 1        | $           | **ACCEPT**          |

### Test 2: Illegitimate Input `+ i i`

**Expected:** ERROR ✓

**Parsing Trace:**

| Step | Stack | Input     | Action           |
|------|-------|-----------|------------------|
| 0    | 0     | + i i $   | **ERROR** - no action for (+, state 0) |

The parser correctly rejects this input because there is no valid action in state 0 for the lookahead `+`.

---

## Implementation Notes

- The parser is implemented in `lr_parser_template.py`
- Uses a stack-based table-driven approach
- ACTION table handles shift/reduce/accept decisions
- GOTO table handles nonterminal transitions after reductions
- All test cases pass successfully

---

## Conclusion

The SLR(1) parser successfully handles Grammar 8B, which contains left recursion (`E → E + T`). This grammar is **not** suitable for LL(1) parsing due to the left recursion, but works perfectly with bottom-up LR parsing.

The parser correctly:
- ✓ Accepts valid expressions like `i`, `i + i`, `i + i + i`
- ✓ Rejects invalid expressions like `+ i i`, `i +`

