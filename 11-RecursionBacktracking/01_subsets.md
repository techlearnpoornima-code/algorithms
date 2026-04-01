# Subsets

## 1. Problem Statement
Given an integer array `nums` of **unique** elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets.

- **Input:** `nums` (integer array)
- **Output:** List of all subsets

---

## 2. Example
```
Input:  nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

---

## 3. Iterative Approach (Bit Manipulation)

```python
def subsets_iter(nums):
    result = [[]]
    for num in nums:
        result += [subset + [num] for subset in result]
    return result
```

- **Time Complexity:** O(2^n × n)
- **Space Complexity:** O(2^n × n)

---

## 4. Optimized Approach (Backtracking)

**Key Idea:**
- At each index, make a binary choice: include or exclude the current element.
- Collect each state of the `current` path as a valid subset.

```python
def subsets(nums):
    result = []

    def backtrack(start, current):
        result.append(list(current))  # every state is a valid subset
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()  # undo choice

    backtrack(0, [])
    return result
```

- **Time Complexity:** O(2^n × n)
- **Space Complexity:** O(n) — recursion depth

---

## 5. Code Walkthrough

**Input:** `nums = [1,2,3]`

Backtracking tree:
```
start=0, curr=[]       → add []
  add 1, curr=[1]      → add [1]
    add 2, curr=[1,2]  → add [1,2]
      add 3 → add [1,2,3], pop
    pop → [1]
    add 3, curr=[1,3]  → add [1,3], pop
  pop → []
  add 2, curr=[2]      → add [2]
    add 3 → add [2,3], pop
  pop → []
  add 3, curr=[3]      → add [3]
```

**Output:** `[[], [1], [1,2], [1,2,3], [1,3], [2], [2,3], [3]]`
