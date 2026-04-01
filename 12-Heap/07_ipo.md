# IPO

## 1. Problem Statement
Given `k` projects you can complete, each with `profits[i]` and `capital[i]` required, find the **maximum capital** after completing at most `k` projects. Start with capital `w`.

---

## 2. Example
```
Input:  k=2, w=0, profits=[1,2,3], capital=[0,1,1]
Output: 4
```

---

## 3. Approach (Two Heaps)

**Key Idea:**
- Min heap of `(capital, profit)` — sorted by required capital.
- Max heap of profits for currently affordable projects.
- Each round: move all affordable projects to max heap, pick the most profitable.

```python
import heapq

def findMaximizedCapital(k, w, profits, capital):
    min_heap = sorted(zip(capital, profits))  # sorted by capital
    max_heap = []
    i = 0

    for _ in range(k):
        # Add all affordable projects to max heap
        while i < len(min_heap) and min_heap[i][0] <= w:
            heapq.heappush(max_heap, -min_heap[i][1])
            i += 1
        if not max_heap:
            break
        w += -heapq.heappop(max_heap)

    return w
```

- **Time Complexity:** O(n log n + k log n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** k=2, w=0, profits=[1,2,3], capital=[0,1,1]

- Round 1: affordable (capital<=0): project(0,1) → max_heap=[-1] → pick profit=1, w=1
- Round 2: affordable (capital<=1): projects(1,2),(1,3) → max_heap=[-3,-2] → pick profit=3, w=4

**Output:** `4`
