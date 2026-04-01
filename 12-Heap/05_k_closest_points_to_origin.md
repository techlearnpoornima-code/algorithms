# K Closest Points to Origin

## 1. Problem Statement
Given `points` on a plane, return the `k` closest points to the origin `(0,0)`. Distance = √(x²+y²) (no need to sqrt, compare squares).

---

## 2. Example
```
Input:  points=[[1,3],[-2,2]], k=1
Output: [[-2,2]]  (dist²=8 < dist²=10)
```

---

## 3. Approach (Max Heap of Size k)

```python
import heapq

def kClosest(points, k):
    heap = []  # max heap using negative distances
    for x, y in points:
        dist = -(x*x + y*y)
        heapq.heappush(heap, (dist, x, y))
        if len(heap) > k:
            heapq.heappop(heap)
    return [[x, y] for _, x, y in heap]
```

- **Time Complexity:** O(n log k)
- **Space Complexity:** O(k)

---

## 4. Alternative: heapq.nsmallest

```python
def kClosest_simple(points, k):
    return heapq.nsmallest(k, points, key=lambda p: p[0]**2 + p[1]**2)
```
