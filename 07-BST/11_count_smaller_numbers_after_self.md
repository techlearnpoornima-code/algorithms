# Count of Smaller Numbers After Self

## 1. Problem Statement
Given an integer array `nums`, return an array `counts` where `counts[i]` = number of elements to the **right** of `nums[i]` that are smaller than `nums[i]`.

---

## 2. Example
```
Input:  nums = [5,2,6,1]
Output: [2,1,1,0]
  5: [2,6,1] → 2 smaller (2 and 1)
  2: [6,1]   → 1 smaller (1)
  6: [1]     → 1 smaller (1)
  1: []      → 0 smaller
```

---

## 3. Brute Force

```python
def countSmaller_brute(nums):
    return [sum(nums[j] < nums[i] for j in range(i+1, len(nums))) for i in range(len(nums))]
```
- **Time:** O(n²)

---

## 4. Optimized Approach (BST / BIT / Merge Sort)

**Using sorted insertion (BST approach):**

```python
def countSmaller(nums):
    result = []
    sorted_list = []

    for num in reversed(nums):
        # Binary search for insertion position = count of smaller elements
        left, right = 0, len(sorted_list)
        while left < right:
            mid = (left + right) // 2
            if sorted_list[mid] < num:
                left = mid + 1
            else:
                right = mid
        result.append(left)
        sorted_list.insert(left, num)

    return result[::-1]
```

- **Time:** O(n²) worst case with list insert, O(n log n) with BIT/Fenwick tree
- **Space:** O(n)
