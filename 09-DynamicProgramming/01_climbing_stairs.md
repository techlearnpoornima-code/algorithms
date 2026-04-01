# Climbing Stairs

## 1. Problem Statement
You are climbing a staircase with `n` steps. Each time you can climb either **1 or 2 steps**. How many **distinct ways** can you climb to the top?

- **Input:** `n` (integer)
- **Output:** Number of distinct ways

---

## 2. Example
```
Input:  n = 2
Output: 2  (1+1, 2)

Input:  n = 3
Output: 3  (1+1+1, 1+2, 2+1)
```

---

## 3. Brute Force Approach (Recursion)

```python
def climbStairs_brute(n):
    if n <= 2:
        return n
    return climbStairs_brute(n-1) + climbStairs_brute(n-2)
```

- **Time Complexity:** O(2^n) — exponential
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (DP / Fibonacci)

**Key Idea:**
- To reach step `n`, you came from step `n-1` (1 step) or step `n-2` (2 steps).
- So `dp[n] = dp[n-1] + dp[n-2]` — exactly the Fibonacci sequence!
- Base cases: `dp[1]=1`, `dp[2]=2`.

```python
def climbStairs(n):
    if n <= 2:
        return n
    prev2, prev1 = 1, 2
    for _ in range(3, n + 1):
        curr = prev1 + prev2
        prev2 = prev1
        prev1 = curr
    return prev1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `n = 5`

| step | prev2 | prev1 | curr |
|------|-------|-------|------|
| 3    | 1     | 2     | 3    |
| 4    | 2     | 3     | 5    |
| 5    | 3     | 5     | 8    |

**Output:** `8`
