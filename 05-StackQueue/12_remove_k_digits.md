# Remove K Digits

## 1. Problem Statement
Given a string `num` representing a non-negative integer and integer `k`, remove `k` digits to make the **smallest possible number**. Return result as a string without leading zeros.

---

## 2. Example
```
Input:  num="1432219", k=3  → "1219"
Input:  num="10200",   k=1  → "200"  → "200" (no leading zero output: "200")
Input:  num="10",      k=2  → "0"
```

---

## 3. Approach (Monotonic Stack / Greedy)

**Key Idea:**
- To minimize the number, remove digits that are **larger than the next digit** (greedy).
- Use a stack: if current digit < stack top, pop the top (remove it counts as using one of k removals).
- After processing, remove from the end if k still > 0.

```python
def removeKdigits(num, k):
    stack = []

    for digit in num:
        while k and stack and stack[-1] > digit:
            stack.pop()
            k -= 1
        stack.append(digit)

    # If k remaining, remove from end
    stack = stack[:-k] if k else stack

    # Remove leading zeros
    result = ''.join(stack).lstrip('0')
    return result or "0"
```

- **Time:** O(n), **Space:** O(n)

---

## 5. Code Walkthrough

**Input:** `num="1432219"`, `k=3`

| digit | stack      | k  |
|-------|------------|-----|
| 1     | [1]        | 3   |
| 4     | [1,4]      | 3   |
| 3     | [1,3]      | 2 (popped 4) |
| 2     | [1,2]      | 1 (popped 3) |
| 2     | [1,2,2]    | 1   |
| 1     | [1,2,1]    | 0 (popped 2) |
| 9     | [1,2,1,9]  | 0   |

**Output:** `"1219"`
