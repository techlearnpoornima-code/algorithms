# Last Stone Weight

## 1. Problem Statement
Stones with weights; each turn smash the two heaviest. If equal, both destroyed. If unequal, difference survives. Return the weight of the last stone (or 0).

---

## 2. Example
```
Input:  stones = [2,7,4,1,8,1]
Output: 1
```

---

## 3. Approach (Max Heap)

```python
import heapq

def lastStoneWeight(stones):
    heap = [-s for s in stones]  # negate for max heap
    heapq.heapify(heap)

    while len(heap) > 1:
        first = -heapq.heappop(heap)
        second = -heapq.heappop(heap)
        if first != second:
            heapq.heappush(heap, -(first - second))

    return -heap[0] if heap else 0
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `[2,7,4,1,8,1]`

- Heap: [-8,-7,-4,-2,-1,-1]
- Pop 8,7: diff=1, push -1
- Pop 4,2: diff=2, push -2
- Pop 2,1: diff=1, push -1
- Pop 1,1: equal, both gone
- Pop 1: last stone

**Output:** `1`
