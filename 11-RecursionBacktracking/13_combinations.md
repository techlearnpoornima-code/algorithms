# Combinations

## 1. Problem Statement
Given two integers `n` and `k`, return all possible combinations of `k` numbers chosen from the range `[1, n]`.

---

## 2. Example
```
Input:  n=4, k=2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
```

---

## 3. Approach (Backtracking)

```python
def combine(n, k):
    result = []

    def backtrack(start, current):
        if len(current) == k:
            result.append(list(current))
            return
        # Pruning: need at least k-len(current) more elements
        for i in range(start, n - (k - len(current)) + 2):
            current.append(i)
            backtrack(i + 1, current)
            current.pop()

    backtrack(1, [])
    return result
```

- **Time:** O(C(n,k) × k), **Space:** O(k)

---

## 5. Code Walkthrough

**n=4, k=2:**

```
start=1: [1] → start=2: [1,2]✅ [1,3]✅ [1,4]✅
start=2: [2] → start=3: [2,3]✅ [2,4]✅
start=3: [3] → start=4: [3,4]✅
```

**Output:** `[[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]`
