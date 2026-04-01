# Letter Combinations of a Phone Number

## 1. Problem Statement
Given a string of digits (2-9), return all possible letter combinations using a phone keypad.

---

## 2. Example
```
Input:  digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

---

## 3. Approach (Backtracking)

```python
def letterCombinations(digits):
    if not digits: return []
    mapping = {'2':'abc','3':'def','4':'ghi','5':'jkl',
               '6':'mno','7':'pqrs','8':'tuv','9':'wxyz'}
    result = []

    def backtrack(idx, current):
        if idx == len(digits):
            result.append(current)
            return
        for char in mapping[digits[idx]]:
            backtrack(idx + 1, current + char)

    backtrack(0, "")
    return result
```

- **Time Complexity:** O(4^n × n)
- **Space Complexity:** O(n)
