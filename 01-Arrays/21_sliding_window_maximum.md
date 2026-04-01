# Sliding Window Maximum

## 1. Problem Statement
Given an array `nums` and a sliding window of size `k`, return the **maximum value in each window** as it slides from left to right.

- **Input:** `nums` (integer array), `k` (integer)
- **Output:** Array of window maximums

---

## 2. Example
```
Input:  nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
```

---

## 3. Brute Force

```python
def maxSlidingWindow_brute(nums, k):
    return [max(nums[i:i+k]) for i in range(len(nums)-k+1)]
```

- **Time Complexity:** O(n × k)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Monotonic Deque)

**Key Idea:**
- Use a deque storing **indices** in decreasing order of their values.
- The front of the deque is always the index of the current window's maximum.
- Remove indices that are out of window from the front.
- Remove indices from the back whose values are smaller than current (they'll never be max).

```python
from collections import deque

def maxSlidingWindow(nums, k):
    dq = deque()  # stores indices, decreasing values
    result = []

    for i, num in enumerate(nums):
        # Remove out-of-window indices from front
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        # Remove smaller values from back
        while dq and nums[dq[-1]] < num:
            dq.pop()

        dq.append(i)

        if i >= k - 1:
            result.append(nums[dq[0]])

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(k)

---

## 5. Code Walkthrough

**Input:** `nums=[1,3,-1,-3,5,3,6,7]`, `k=3`

| i | num | dq (indices) | window max |
|---|-----|-------------|------------|
| 0 | 1   | [0]         | —          |
| 1 | 3   | [1]         | —          |
| 2 | -1  | [1,2]       | nums[1]=3  |
| 3 | -3  | [1,2,3]     | nums[1]=3  |
| 4 | 5   | [4]         | nums[4]=5  |
| 5 | 3   | [4,5]       | nums[4]=5  |
| 6 | 6   | [6]         | nums[6]=6  |
| 7 | 7   | [7]         | nums[7]=7  |

**Output:** `[3,3,5,5,6,7]`
