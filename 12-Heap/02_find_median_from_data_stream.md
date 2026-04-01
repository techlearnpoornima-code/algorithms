# Find Median from Data Stream

## 1. Problem Statement
Design a data structure that supports:
- `addNum(num)`: Add a number to the data structure.
- `findMedian()`: Return the median of all added numbers.

- **Input:** Stream of integers
- **Output:** Median after each addition

---

## 2. Example
```
addNum(1) → [1]          findMedian() → 1.0
addNum(2) → [1,2]        findMedian() → 1.5
addNum(3) → [1,2,3]      findMedian() → 2.0
```

---

## 3. Brute Force Approach

```python
class MedianFinder_brute:
    def __init__(self):
        self.data = []

    def addNum(self, num):
        self.data.append(num)

    def findMedian(self):
        self.data.sort()
        n = len(self.data)
        if n % 2 == 1:
            return float(self.data[n//2])
        return (self.data[n//2 - 1] + self.data[n//2]) / 2.0
```

- **addNum:** O(1), **findMedian:** O(n log n)

---

## 4. Optimized Approach (Two Heaps)

**Key Idea:**
- Maintain two heaps:
  - `small`: max-heap (inverted) for the lower half
  - `large`: min-heap for the upper half
- Keep them balanced: `|small| - |large| <= 1`.
- Median = top of `small` (odd total) or average of tops (even total).

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small = []  # max-heap (negate values)
        self.large = []  # min-heap

    def addNum(self, num):
        heapq.heappush(self.small, -num)
        # Ensure all small <= all large
        if self.small and self.large and (-self.small[0]) > self.large[0]:
            heapq.heappush(self.large, -heapq.heappop(self.small))
        # Balance sizes
        if len(self.small) > len(self.large) + 1:
            heapq.heappush(self.large, -heapq.heappop(self.small))
        elif len(self.large) > len(self.small):
            heapq.heappush(self.small, -heapq.heappop(self.large))

    def findMedian(self):
        if len(self.small) > len(self.large):
            return float(-self.small[0])
        return (-self.small[0] + self.large[0]) / 2.0
```

- **addNum:** O(log n), **findMedian:** O(1)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Operations:** addNum(1), addNum(2), addNum(3)

| op         | small (max-heap) | large (min-heap) | median |
|------------|------------------|------------------|--------|
| addNum(1)  | [-1]             | []               | 1.0    |
| addNum(2)  | [-1]             | [2]              | 1.5    |
| addNum(3)  | [-2,-1]          | [3]              | 2.0    |

- After addNum(3): small=[-2,-1] (top=-(-2)=2), large=[3]
- Median = -small[0] = 2.0
