# Binary Search

## 1. Problem Statement
Given a sorted array `nums` and a `target`, return the index of `target` if found. If not present, return `-1`. Must run in O(log n).

- **Input:** `nums` (sorted integer array), `target` (integer)
- **Output:** Index of target, or -1

---

## 2. Example
```
Input:  nums = [-1,0,3,5,9,12], target = 9
Output: 4

Input:  nums = [-1,0,3,5,9,12], target = 2
Output: -1
```

---

## 3. Brute Force Approach

```python
def search_brute(nums, target):
    for i, num in enumerate(nums):
        if num == target:
            return i
    return -1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Binary Search)

**Key Idea:**
- Maintain `left` and `right` pointers.
- Compare target with the middle element: if equal → found; if less → search left half; if greater → search right half.

```python
def search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [-1,0,3,5,9,12]`, `target = 9`

| left | right | mid | nums[mid] | action      |
|------|-------|-----|-----------|-------------|
| 0    | 5     | 2   | 3         | 3 < 9 → left=3 |
| 3    | 5     | 4   | 9         | found! return 4 |

**Output:** `4`
