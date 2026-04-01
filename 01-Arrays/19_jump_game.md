# Jump Game

## 1. Problem Statement
Given an integer array `nums` where `nums[i]` is the maximum jump length from index `i`, return `true` if you can reach the last index starting from index `0`.

- **Input:** `nums` (integer array)
- **Output:** Boolean

---

## 2. Example
```
Input:  nums = [2,3,1,1,4]
Output: true

Input:  nums = [3,2,1,0,4]
Output: false  (always stuck at index 3)
```

---

## 3. Brute Force (BFS/DFS)

```python
def canJump_brute(nums):
    reachable = {0}
    for i in range(len(nums)):
        if i in reachable:
            for j in range(1, nums[i]+1):
                reachable.add(i+j)
    return len(nums)-1 in reachable
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Greedy)

**Key Idea:**
- Track the farthest index reachable (`max_reach`) as we iterate.
- If we ever reach a position beyond `max_reach`, we're stuck — return False.
- If `max_reach` reaches or passes the last index, return True.

```python
def canJump(nums):
    max_reach = 0
    for i, jump in enumerate(nums):
        if i > max_reach:
            return False  # can't reach this position
        max_reach = max(max_reach, i + jump)
    return True
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [3,2,1,0,4]`

| i | nums[i] | max_reach | i > max_reach? |
|---|---------|-----------|----------------|
| 0 | 3       | 3         | No             |
| 1 | 2       | 3         | No             |
| 2 | 1       | 3         | No             |
| 3 | 0       | 3         | No             |
| 4 | 4       | 3         | Yes → False ❌ |

**Output:** `False`
