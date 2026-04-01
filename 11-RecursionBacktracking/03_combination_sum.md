# Combination Sum

## 1. Problem Statement
Given an array of **distinct** integers `candidates` and a `target`, return all unique combinations where the candidates sum to target. The **same number may be used multiple times**.

- **Input:** `candidates` (integer array), `target` (integer)
- **Output:** List of all combinations

---

## 2. Example
```
Input:  candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

Input:  candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

---

## 3. Approach (Backtracking)

**Key Idea:**
- At each step, try each candidate starting from index `start` (to avoid duplicate combinations in different orders).
- Subtract the candidate from the remaining target.
- Stop when target reaches 0 (found!) or goes negative.

```python
def combinationSum(candidates, target):
    result = []
    candidates.sort()

    def backtrack(start, current, remaining):
        if remaining == 0:
            result.append(list(current))
            return
        for i in range(start, len(candidates)):
            if candidates[i] > remaining:
                break  # sorted, so no point continuing
            current.append(candidates[i])
            backtrack(i, current, remaining - candidates[i])  # i not i+1, reuse allowed
            current.pop()

    backtrack(0, [], target)
    return result
```

- **Time Complexity:** O(N^(T/M)) — N=candidates, T=target, M=min candidate
- **Space Complexity:** O(T/M) — recursion depth

---

## 5. Code Walkthrough

**Input:** `candidates = [2,3,6,7]`, `target = 7`

```
backtrack(0, [], 7)
  try 2 → backtrack(0, [2], 5)
    try 2 → backtrack(0, [2,2], 3)
      try 2 → backtrack(0, [2,2,2], 1)
        try 2 → remaining=-1 → stop
        try 3 → remaining=-2 → stop
      try 3 → backtrack(1, [2,2,3], 0) → add [2,2,3] ✅
    try 3 → backtrack(1, [2,3], 2)
      try 3 → remaining=-1 → stop
  try 3 → backtrack(1, [3], 4) → ...
  try 6 → backtrack(2, [6], 1) → stop
  try 7 → backtrack(3, [7], 0) → add [7] ✅
```

**Output:** `[[2,2,3],[7]]`
