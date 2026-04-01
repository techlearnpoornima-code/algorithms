# Kth Largest Element in an Array

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the **k-th largest** element in the array (not distinct — kth position in sorted order).

- **Input:** `nums` (integer array), `k` (integer)
- **Output:** k-th largest element

---

## 2. Example
```
Input:  nums = [3,2,1,5,6,4], k = 2
Output: 5

Input:  nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

---

## 3. Brute Force Approach

```python
def findKthLargest_brute(nums, k):
    nums.sort(reverse=True)
    return nums[k-1]
```

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Min-Heap of Size k)

**Key Idea:**
- Maintain a min-heap of size `k`.
- The smallest element in the heap is always the k-th largest seen so far.
- If heap size exceeds k, pop the minimum (too small to be top-k).

```python
import heapq

def findKthLargest(nums, k):
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)  # remove smallest
    return heap[0]  # kth largest = smallest in top-k heap
```

- **Time Complexity:** O(n log k)
- **Space Complexity:** O(k)

---

## 5. Code Walkthrough

**Input:** `nums = [3,2,1,5,6,4]`, `k = 2`

| num | heap (before pop) | after pop | heap |
|-----|-------------------|-----------|------|
| 3   | [3]               | —         | [3] |
| 2   | [2,3]             | —         | [2,3] |
| 1   | [1,3,2]           | pop 1     | [2,3] |
| 5   | [2,3,5]           | —         | [2,3,5] |
| 6   | [2,3,5,6]         | pop 2     | [3,5,6] |
| 4   | [3,5,6,4]         | pop 3     | [4,5,6] |

`heap[0] = 4`? No wait — `k=2` so heap keeps 2 largest.

Re-run: heap of size 2 → final heap = [5,6], heap[0] = **5**

**Output:** `5`
