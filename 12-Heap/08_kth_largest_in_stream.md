# Kth Largest Element in a Stream

## 1. Problem Statement
Design a class `KthLargest` that finds the **k-th largest** element in a stream. It has:
- `KthLargest(k, nums)`: Initialize with k and initial numbers.
- `add(val)`: Add val and return the k-th largest element.

---

## 2. Example
```
KthLargest(3, [4,5,8,2])
add(3)  → 4   (stream: [2,3,4,5,8], 3rd largest = 4)
add(5)  → 5
add(10) → 5
add(9)  → 8
add(4)  → 8
```

---

## 3. Approach (Min-Heap of Size k)

**Key Idea:**
- Maintain a min-heap of size k.
- The heap's minimum = k-th largest element.

```python
import heapq

class KthLargest:
    def __init__(self, k, nums):
        self.k = k
        self.heap = []
        for num in nums:
            self.add(num)

    def add(self, val):
        heapq.heappush(self.heap, val)
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)
        return self.heap[0]
```

- **add:** O(log k), **Space:** O(k)
