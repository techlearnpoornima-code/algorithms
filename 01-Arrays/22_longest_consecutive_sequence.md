# Longest Consecutive Sequence

## 1. Problem Statement
Given an unsorted array of integers `nums`, return the length of the **longest consecutive elements sequence**. Must run in O(n).

- **Input:** `nums` (integer array)
- **Output:** Length of longest consecutive sequence

---

## 2. Example
```
Input:  nums = [100,4,200,1,3,2]
Output: 4  (sequence [1,2,3,4])

Input:  nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

---

## 3. Brute Force

```python
def longestConsecutive_brute(nums):
    best = 0
    num_set = set(nums)
    for num in num_set:
        length = 1
        while num + length in num_set:
            length += 1
        best = max(best, length)
    return best
```

- **Time Complexity:** O(n²) worst case
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (HashSet + Sequence Start Detection)

**Key Idea:**
- Add all numbers to a set.
- Only start counting a sequence from a number `n` where `n-1` is NOT in the set (i.e., it's the sequence start).
- This ensures each sequence is counted only once.

```python
def longestConsecutive(nums):
    num_set = set(nums)
    best = 0

    for num in num_set:
        if num - 1 not in num_set:  # start of a sequence
            length = 1
            while num + length in num_set:
                length += 1
            best = max(best, length)

    return best
```

- **Time Complexity:** O(n) — each number visited at most twice
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [100,4,200,1,3,2]`

num_set = {100,4,200,1,3,2}

- num=100: 99 not in set → count: 100 → length=1
- num=4: 3 IS in set → skip (not sequence start)
- num=200: 199 not in set → length=1
- num=1: 0 not in set → count 1,2,3,4 → length=4 ✅
- num=3: 2 IS in set → skip
- num=2: 1 IS in set → skip

**Output:** `4`
