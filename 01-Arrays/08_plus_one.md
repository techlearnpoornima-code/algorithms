# Plus One

## 1. Problem Statement
Given a large integer represented as an array of digits `digits` (most significant digit first), increment the integer by one and return the resulting array of digits.

- **Input:** `digits` (integer array, each element is 0–9)
- **Output:** Modified digits array after adding 1

---

## 2. Example
```
Input:  digits = [1, 2, 3]
Output: [1, 2, 4]
Explanation: 123 + 1 = 124

Input:  digits = [9, 9, 9]
Output: [1, 0, 0, 0]
Explanation: 999 + 1 = 1000
```

---

## 3. Brute Force Approach

**Logic:**
- Convert array to integer, add 1, convert back to array.

```python
def plusOne_brute(digits):
    num = int("".join(map(str, digits)))
    num += 1
    return [int(d) for d in str(num)]
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)
- **Drawback:** Doesn't scale for extremely large integers (integer overflow in some languages)

---

## 4. Optimized Approach (Carry Propagation)

**Key Idea:**
- Traverse from the last digit to the first.
- If digit < 9: just add 1 and return (no carry).
- If digit == 9: set it to 0 and carry over to next digit.
- If we exit the loop with all 9s, prepend a 1.

```python
def plusOne(digits):
    for i in range(len(digits) - 1, -1, -1):
        if digits[i] < 9:
            digits[i] += 1
            return digits
        digits[i] = 0  # carry: 9 + 1 = 10, write 0

    return [1] + digits  # all digits were 9
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) amortized, O(n) in the all-9s edge case

---

## 5. Code Walkthrough

**Input:** `digits = [9, 9, 9]`

| i | digits[i] | Action            | digits     |
|---|-----------|-------------------|------------|
| 2 | 9         | Set to 0, carry   | [9, 9, 0]  |
| 1 | 9         | Set to 0, carry   | [9, 0, 0]  |
| 0 | 9         | Set to 0, carry   | [0, 0, 0]  |
| — | loop ends | Prepend 1         | [1, 0, 0, 0] |

**Output:** `[1, 0, 0, 0]`
