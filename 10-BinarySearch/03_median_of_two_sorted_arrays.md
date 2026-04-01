# Median of Two Sorted Arrays

## 1. Problem Statement
Given two sorted arrays `nums1` and `nums2` of sizes `m` and `n`, return the **median** of the combined sorted array. Must run in O(log(m+n)).

- **Input:** `nums1`, `nums2` (sorted integer arrays)
- **Output:** Median (float)

---

## 2. Example
```
Input:  nums1 = [1,3], nums2 = [2]
Output: 2.0

Input:  nums1 = [1,2], nums2 = [3,4]
Output: 2.5
```

---

## 3. Brute Force Approach

```python
def findMedianSortedArrays_brute(nums1, nums2):
    merged = sorted(nums1 + nums2)
    n = len(merged)
    if n % 2 == 1:
        return float(merged[n // 2])
    return (merged[n//2 - 1] + merged[n//2]) / 2.0
```

- **Time Complexity:** O((m+n) log(m+n))
- **Space Complexity:** O(m+n)

---

## 4. Optimized Approach (Binary Search on Partition)

**Key Idea:**
- Partition both arrays such that left halves combined contain the first half of all elements.
- Binary search on the smaller array to find the correct partition point.
- Median is determined by the max of left parts and min of right parts.

```python
def findMedianSortedArrays(nums1, nums2):
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1  # ensure nums1 is smaller

    m, n = len(nums1), len(nums2)
    left, right = 0, m

    while left <= right:
        i = (left + right) // 2          # partition in nums1
        j = (m + n + 1) // 2 - i        # partition in nums2

        max_left1  = nums1[i-1] if i > 0 else float('-inf')
        min_right1 = nums1[i]   if i < m else float('inf')
        max_left2  = nums2[j-1] if j > 0 else float('-inf')
        min_right2 = nums2[j]   if j < n else float('inf')

        if max_left1 <= min_right2 and max_left2 <= min_right1:
            if (m + n) % 2 == 1:
                return float(max(max_left1, max_left2))
            return (max(max_left1, max_left2) + min(min_right1, min_right2)) / 2.0
        elif max_left1 > min_right2:
            right = i - 1
        else:
            left = i + 1
```

- **Time Complexity:** O(log(min(m,n)))
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums1 = [1,2]`, `nums2 = [3,4]`

- m=2, n=2; binary search on nums1
- i=1, j=1: max_left1=1, min_right1=2, max_left2=3, min_right2=4
  - 1 <= 4 ✅ but 3 > 2 ❌ → left = 2
- i=2, j=0: max_left1=2, min_right1=inf, max_left2=-inf, min_right2=3
  - 2 <= 3 ✅ and -inf <= inf ✅ → even length
  - median = (max(2,-inf) + min(inf,3)) / 2 = (2+3)/2 = 2.5

**Output:** `2.5`
