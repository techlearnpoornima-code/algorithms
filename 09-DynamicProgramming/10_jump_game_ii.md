# Jump Game II

## 1. Problem Statement
Given an integer array `nums` where `nums[i]` is max jump length, return the **minimum number of jumps** to reach the last index. It is guaranteed you can reach.

---

## 2. Example
```
Input:  nums = [2,3,1,1,4]
Output: 2  (jump to index 1, then to end)
```

---

## 3. Approach (Greedy BFS)

**Key Idea:**
- Think of each "jump" as a BFS level.
- Track `current_end` (farthest reachable with current jumps) and `farthest` (farthest reachable overall).
- When we reach `current_end`, increment jumps and extend to `farthest`.

```python
def jump(nums):
    jumps = 0
    current_end = 0
    farthest = 0

    for i in range(len(nums) - 1):
        farthest = max(farthest, i + nums[i])
        if i == current_end:
            jumps += 1
            current_end = farthest

    return jumps
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [2,3,1,1,4]`

| i | nums[i] | farthest | current_end | jumps |
|---|---------|----------|-------------|-------|
| 0 | 2       | 2        | 0→2         | 1     |
| 1 | 3       | 4        | 2           | 1     |
| 2 | 1       | 4        | 2→4         | 2     |
| 3 | 1       | 4        | 4           | 2     |

**Output:** `2`
