# Find K Pairs with Smallest Sums

## 1. Problem Statement
Given two sorted arrays `nums1` and `nums2`, define a pair `(u, v)` from each array. Return the `k` pairs with the **smallest sums**.

---

## 2. Example
```
Input:  nums1=[1,7,11], nums2=[2,4,6], k=3
Output: [[1,2],[1,4],[1,6]]
```

---

## 3. Approach (Min-Heap)

**Key Idea:**
- Start by pushing all pairs with `nums1[i]` and `nums2[0]` into a min-heap.
- Each time we pop `(sum, i, j)`, push `(nums1[i]+nums2[j+1], i, j+1)` for the next element.

```python
import heapq

def kSmallestPairs(nums1, nums2, k):
    if not nums1 or not nums2: return []
    heap = [(nums1[i] + nums2[0], i, 0) for i in range(min(k, len(nums1)))]
    heapq.heapify(heap)
    result = []

    while heap and len(result) < k:
        _, i, j = heapq.heappop(heap)
        result.append([nums1[i], nums2[j]])
        if j + 1 < len(nums2):
            heapq.heappush(heap, (nums1[i] + nums2[j+1], i, j+1))

    return result
```

- **Time:** O(k log k), **Space:** O(k)

---

## 5. Code Walkthrough

**Input:** `nums1=[1,7,11]`, `nums2=[2,4,6]`, `k=3`

Initial heap: [(3,0,0),(9,1,0),(13,2,0)]

| pop       | result       | push        |
|-----------|-------------|-------------|
| (3,0,0)   | [1,2]       | (5,0,1)     |
| (5,0,1)   | [1,4]       | (7,0,2)     |
| (7,0,2)   | [1,6]       | —           |

**Output:** `[[1,2],[1,4],[1,6]]`
