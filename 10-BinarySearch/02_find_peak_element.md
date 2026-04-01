# Find Peak Element

## 1. Problem Statement
A peak element is one that is greater than its neighbors. Given `nums`, find a peak element and return its index. You may assume `nums[-1] = nums[n] = -∞`. Must run in O(log n).

- **Input:** `nums` (integer array)
- **Output:** Index of any peak element

---

## 2. Example
```
Input:  nums = [1,2,3,1]
Output: 2  (nums[2]=3 is a peak)

Input:  nums = [1,2,1,3,5,6,4]
Output: 5  (nums[5]=6 is a peak)
```

---

## 3. Brute Force

```python
def findPeakElement_brute(nums):
    for i in range(len(nums)):
        if (i == 0 or nums[i] > nums[i-1]) and (i == len(nums)-1 or nums[i] > nums[i+1]):
            return i
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Binary Search)

**Key Idea:**
- Compare `nums[mid]` with `nums[mid+1]`.
- If `nums[mid] < nums[mid+1]`: there's a peak to the right → `left = mid+1`.
- Otherwise: there's a peak at mid or to the left → `right = mid`.
- The intuition: we always move toward the upward slope.

```python
def findPeakElement(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2
        if nums[mid] < nums[mid + 1]:
            left = mid + 1  # peak is to the right
        else:
            right = mid     # peak is at mid or to the left

    return left
```

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [1,2,1,3,5,6,4]`

| left | right | mid | nums[mid] | nums[mid+1] | action |
|------|-------|-----|-----------|-------------|--------|
| 0    | 6     | 3   | 3         | 5           | 3<5 → left=4 |
| 4    | 6     | 5   | 6         | 4           | 6>4 → right=5 |
| 4    | 5     | 4   | 5         | 6           | 5<6 → left=5 |
| 5    | 5     | —   | —         | —           | left==right, stop |

**Output:** `5`
