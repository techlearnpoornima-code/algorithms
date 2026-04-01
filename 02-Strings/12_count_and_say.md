# Count and Say

## 1. Problem Statement
The **count-and-say** sequence is built by reading the previous term aloud: count consecutive digits and say how many of each. Return the `n`-th term.

- **Input:** `n` (integer)
- **Output:** n-th term as string

---

## 2. Example
```
1 → "1"
2 → "11"       (one 1)
3 → "21"       (two 1s)
4 → "1211"     (one 2, one 1)
5 → "111221"   (one 1, one 2, two 1s)
```

---

## 3. Approach (Iterative)

```python
def countAndSay(n):
    result = "1"
    for _ in range(n - 1):
        next_str = ""
        i = 0
        while i < len(result):
            count = 1
            while i + count < len(result) and result[i+count] == result[i]:
                count += 1
            next_str += str(count) + result[i]
            i += count
        result = next_str
    return result
```

- **Time Complexity:** O(n × m) where m = length of current term
- **Space Complexity:** O(m)

---

## 5. Code Walkthrough

**n = 4**, start from "1":

- "1" → one 1 → "11"
- "11" → two 1s → "21"
- "21" → one 2, one 1 → "1211"

**Output:** `"1211"`
