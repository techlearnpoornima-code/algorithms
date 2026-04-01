# Top K Frequent Elements (Heap Approach)

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements using a heap.

> See also: `03-Hashing/05_top_k_frequent_elements.md` for bucket sort approach.

---

## 2. Example
```
Input:  nums = [1,1,1,2,2,3], k = 2
Output: [1, 2]
```

---

## 3. Optimized Approach (Min-Heap)

**Key Idea:**
- Count frequencies with a hashmap.
- Use a min-heap of size `k` based on frequency.
- Maintain only the `k` most frequent elements.

```python
import heapq
from collections import Counter

def topKFrequent(nums, k):
    count = Counter(nums)
    # min-heap: (frequency, num)
    heap = []

    for num, freq in count.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)  # remove least frequent

    return [num for freq, num in heap]
```

- **Time Complexity:** O(n log k)
- **Space Complexity:** O(n + k)

---

## 4. Using heapq.nlargest (Pythonic)

```python
def topKFrequent_nlargest(nums, k):
    count = Counter(nums)
    return heapq.nlargest(k, count.keys(), key=count.get)
```

- **Time Complexity:** O(n log k)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [1,1,1,2,2,3]`, `k = 2`

count: `{1:3, 2:2, 3:1}`

Heap operations:
- push (3,1): heap=[(3,1)]
- push (2,2): heap=[(2,2),(3,1)]  (min-heap ordered by freq)
- push (1,3): heap=[(1,3),(3,1),(2,2)] → size=3 > k=2 → pop min (1,3)
- Final heap: [(2,2),(3,1)]

Result: [1, 2]

**Output:** `[1, 2]`
