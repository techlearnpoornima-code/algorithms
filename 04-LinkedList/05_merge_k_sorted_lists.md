# Merge K Sorted Lists

## 1. Problem Statement
Given an array of `k` sorted linked lists, merge them into one sorted linked list and return its head.

- **Input:** `lists` (array of ListNode heads)
- **Output:** Head of merged sorted linked list

---

## 2. Example
```
Input:  lists = [[1→4→5], [1→3→4], [2→6]]
Output: 1→1→2→3→4→4→5→6
```

---

## 3. Brute Force Approach

```python
def mergeKLists_brute(lists):
    vals = []
    for node in lists:
        while node:
            vals.append(node.val)
            node = node.next
    vals.sort()
    dummy = ListNode(0)
    curr = dummy
    for v in vals:
        curr.next = ListNode(v)
        curr = curr.next
    return dummy.next
```

- **Time Complexity:** O(N log N) where N = total nodes
- **Space Complexity:** O(N)

---

## 4. Optimized Approach (Min Heap)

**Key Idea:**
- Use a min-heap of size k. Initially push the head of each list.
- Repeatedly pop the smallest node, add it to result, and push its next node.

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

- **Time Complexity:** O(N log k)
- **Space Complexity:** O(k)

---

## 5. Code Walkthrough

**Input:** `[[1→4→5], [1→3→4], [2→6]]`

Initial heap: `[(1,0,node1), (1,1,node1'), (2,2,node2)]`

| pop      | push       | result         |
|----------|------------|----------------|
| (1,0,1)  | (4,0,4)    | 1              |
| (1,1,1)  | (3,1,3)    | 1→1            |
| (2,2,2)  | (6,2,6)    | 1→1→2          |
| (3,1,3)  | (4,1,4)    | 1→1→2→3        |
| (4,0,4)  | (5,0,5)    | 1→1→2→3→4      |
| (4,1,4)  | none       | 1→1→2→3→4→4    |
| (5,0,5)  | none       | 1→1→2→3→4→4→5  |
| (6,2,6)  | none       | 1→1→2→3→4→4→5→6|

**Output:** `1→1→2→3→4→4→5→6`
