# Permutations

## 1. Problem Statement
Given an array `nums` of **distinct** integers, return all possible permutations.

- **Input:** `nums` (integer array)
- **Output:** List of all permutations

---

## 2. Example
```
Input:  nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

---

## 3. Approach (Backtracking)

**Key Idea:**
- At each position, try each unused number.
- Use a `used` set to track which numbers are in the current permutation.
- When the permutation length equals `n`, record it.

```python
def permute(nums):
    result = []
    n = len(nums)

    def backtrack(current, used):
        if len(current) == n:
            result.append(list(current))
            return
        for num in nums:
            if num not in used:
                current.append(num)
                used.add(num)
                backtrack(current, used)
                current.pop()
                used.remove(num)

    backtrack([], set())
    return result
```

- **Time Complexity:** O(n! × n)
- **Space Complexity:** O(n)

---

## 4. Swap-Based Approach

```python
def permute_swap(nums):
    result = []

    def backtrack(start):
        if start == len(nums):
            result.append(list(nums))
            return
        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]  # restore

    backtrack(0)
    return result
```

- **Time Complexity:** O(n! × n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [1,2,3]`

```
backtrack([], {})
  try 1 → backtrack([1], {1})
    try 2 → backtrack([1,2], {1,2})
      try 3 → backtrack([1,2,3]) → add [1,2,3]
    try 3 → backtrack([1,3], {1,3})
      try 2 → backtrack([1,3,2]) → add [1,3,2]
  try 2 → backtrack([2], {2}) → ... [2,1,3], [2,3,1]
  try 3 → ... [3,1,2], [3,2,1]
```

**Output:** All 6 permutations
