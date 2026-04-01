# Intersection of Two Arrays

## 1. Problem Statement
Given two integer arrays `nums1` and `nums2`, return an array of their **intersection** — elements that appear in both arrays. Each element in the result must be **unique**.

- **Input:** `nums1`, `nums2` (integer arrays)
- **Output:** Array of unique common elements (order doesn't matter)

---

## 2. Example
```
Input:  nums1 = [1, 2, 2, 1], nums2 = [2, 2]
Output: [2]

Input:  nums1 = [4, 9, 5], nums2 = [9, 4, 9, 8, 4]
Output: [9, 4]
```

---

## 3. Brute Force Approach

**Logic:**
- For each element in `nums1`, check if it exists in `nums2`.
- Use a result set to avoid duplicates.

```python
def intersection_brute(nums1, nums2):
    result = set()
    for num in nums1:
        if num in nums2:
            result.add(num)
    return list(result)
```

- **Time Complexity:** O(n × m) — `in` on a list is O(m)
- **Space Complexity:** O(min(n, m)) — result set

---

## 4. Optimized Approach (HashSet)

**Key Idea:**
- Convert `nums1` to a set for O(1) lookups.
- Iterate through `nums2`; if the element is in the set, add to result.

```python
def intersection(nums1, nums2):
    set1 = set(nums1)
    result = set()

    for num in nums2:
        if num in set1:
            result.add(num)

    return list(result)
```

> **One-liner:** `return list(set(nums1) & set(nums2))`

- **Time Complexity:** O(n + m)
- **Space Complexity:** O(n) for the set

---

## 5. Code Walkthrough

**Input:** `nums1 = [4, 9, 5]`, `nums2 = [9, 4, 9, 8, 4]`

- `set1 = {4, 9, 5}`
- Iterate `nums2`:
  - 9 → in set1 → result = {9}
  - 4 → in set1 → result = {9, 4}
  - 9 → already in result → {9, 4}
  - 8 → not in set1 → skip
  - 4 → already in result → {9, 4}

**Output:** `[9, 4]`
