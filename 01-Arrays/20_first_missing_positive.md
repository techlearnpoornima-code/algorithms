# First Missing Positive

## 1. Problem Statement
Given an unsorted integer array `nums`, return the **smallest missing positive integer**. Must run in O(n) time and O(1) extra space.

- **Input:** `nums` (integer array)
- **Output:** Smallest missing positive integer

---

## 2. Example
```
Input:  nums = [1,2,0]
Output: 3

Input:  nums = [3,4,-1,1]
Output: 2

Input:  nums = [7,8,9,11,12]
Output: 1
```

---

## 3. Brute Force

```python
def firstMissingPositive_brute(nums):
    num_set = set(nums)
    i = 1
    while i in num_set:
        i += 1
    return i
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Index as Hash)

**Key Idea:**
- The answer must be in range `[1, n+1]`. Use the array itself as a hash table.
- Place each number `x` (where `1 <= x <= n`) at index `x-1`.
- After rearranging, scan: the first index where `nums[i] != i+1` gives the answer.

```python
def firstMissingPositive(nums):
    n = len(nums)

    # Place each number in its correct position
    for i in range(n):
        while 1 <= nums[i] <= n and nums[nums[i]-1] != nums[i]:
            correct = nums[i] - 1
            nums[i], nums[correct] = nums[correct], nums[i]

    # Find first position where number doesn't match
    for i in range(n):
        if nums[i] != i + 1:
            return i + 1

    return n + 1
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `nums = [3,4,-1,1]`

After placement: `[1,-1,3,4]`
- index 0: nums[0]=1 ✅
- index 1: nums[1]=-1 ≠ 2 → return **2**

**Output:** `2`
