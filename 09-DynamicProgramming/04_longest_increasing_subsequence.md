# Longest Increasing Subsequence

## 1. Problem Statement
Given an integer array `nums`, return the **length of the longest strictly increasing subsequence**.

- **Input:** `nums` (integer array)
- **Output:** Length of LIS

---

## 2. Example
```
Input:  nums = [10,9,2,5,3,7,101,18]
Output: 4  (subsequence [2,3,7,101])

Input:  nums = [0,1,0,3,2,3]
Output: 4
```

---

## 3. Brute Force Approach (DP O(n²))

**Key Idea:**
- `dp[i]` = length of LIS ending at index `i`.
- For each `i`, check all `j < i`: if `nums[j] < nums[i]`, then `dp[i] = max(dp[i], dp[j] + 1)`.

```python
def lengthOfLIS_dp(nums):
    n = len(nums)
    dp = [1] * n  # every element is LIS of length 1 by itself

    for i in range(1, n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Binary Search / Patience Sort)

**Key Idea:**
- Maintain a `tails` array where `tails[i]` = smallest tail element of all increasing subsequences of length `i+1`.
- For each number, binary search for its position in `tails` and replace or extend.

```python
import bisect

def lengthOfLIS(nums):
    tails = []

    for num in nums:
        pos = bisect.bisect_left(tails, num)
        if pos == len(tails):
            tails.append(num)   # extend longest subsequence
        else:
            tails[pos] = num    # replace to keep tails minimal

    return len(tails)
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `[10, 9, 2, 5, 3, 7, 101, 18]`

| num | tails (before) | bisect_left pos | tails (after) |
|-----|----------------|-----------------|---------------|
| 10  | []             | 0 (extend)      | [10]          |
| 9   | [10]           | 0 (replace)     | [9]           |
| 2   | [9]            | 0 (replace)     | [2]           |
| 5   | [2]            | 1 (extend)      | [2,5]         |
| 3   | [2,5]          | 1 (replace)     | [2,3]         |
| 7   | [2,3]          | 2 (extend)      | [2,3,7]       |
| 101 | [2,3,7]        | 3 (extend)      | [2,3,7,101]   |
| 18  | [2,3,7,101]    | 3 (replace)     | [2,3,7,18]    |

Length of tails = **4**

**Output:** `4`
