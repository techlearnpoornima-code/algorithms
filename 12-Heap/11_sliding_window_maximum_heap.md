# Sliding Window Maximum (Heap Approach)

## 1. Problem Statement
Given an array and window size k, return the maximum in each sliding window.

> See full deque solution in `01-Arrays/21_sliding_window_maximum.md`.

---

## 2. Heap-Based Approach

**Key Idea:** Use a max-heap. After each push, check if the heap's top is still within the window.

```python
import heapq

def maxSlidingWindow_heap(nums, k):
    heap = []   # (-val, index)
    result = []

    for i, num in enumerate(nums):
        heapq.heappush(heap, (-num, i))
        # Remove elements outside window
        while heap[0][1] < i - k + 1:
            heapq.heappop(heap)
        if i >= k - 1:
            result.append(-heap[0][0])

    return result
```

- **Time:** O(n log n) — worse than deque O(n) but simpler
- **Space:** O(n)

> **Note:** The monotonic deque approach in Arrays folder is preferred for O(n) time.
