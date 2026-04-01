# Merge K Sorted Lists (Heap Approach)

## 1. Problem Statement
Merge k sorted linked lists into one sorted list using a min-heap.

> See full solution in `04-LinkedList/05_merge_k_sorted_lists.md`.

---

## 2. Key Insight (Heap Perspective)
Use a min-heap of size k. Push the head of each list initially. Each pop gives the current minimum; push the popped node's next to keep the heap populated.

```python
import heapq

def mergeKLists(lists):
    dummy = ListNode(0)
    curr = dummy
    heap = []

    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))

    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))

    return dummy.next
```

- **Time:** O(N log k) — N total nodes, k lists
- **Space:** O(k)
