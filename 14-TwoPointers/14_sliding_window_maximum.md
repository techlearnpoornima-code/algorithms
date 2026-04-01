# Sliding Window Maximum (Sliding Window)

## 1. Problem Statement
Return the maximum of each sliding window of size k.

> See full deque solution in `01-Arrays/21_sliding_window_maximum.md`.

---

## 2. Sliding Window Pattern (Monotonic Deque)

Maintain a deque of indices in decreasing order of values:

```python
from collections import deque

def maxSlidingWindow(nums, k):
    dq = deque()
    result = []
    for i, num in enumerate(nums):
        while dq and dq[0] < i - k + 1: dq.popleft()
        while dq and nums[dq[-1]] < num: dq.pop()
        dq.append(i)
        if i >= k - 1:
            result.append(nums[dq[0]])
    return result
```

- **Time:** O(n), **Space:** O(k)
