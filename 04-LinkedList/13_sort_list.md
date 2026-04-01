# Sort List

## 1. Problem Statement
Sort a linked list in **O(n log n)** time using **O(1)** memory (bottom-up merge sort preferred).

---

## 2. Example
```
Input:  4→2→1→3
Output: 1→2→3→4
```

---

## 3. Approach (Top-Down Merge Sort)

**Key Idea:** Split list at midpoint, recursively sort each half, merge.

```python
def sortList(head):
    if not head or not head.next:
        return head

    # Find middle and split
    slow, fast = head, head.next
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    mid = slow.next
    slow.next = None

    left = sortList(head)
    right = sortList(mid)
    return merge(left, right)

def merge(l1, l2):
    dummy = ListNode(0)
    curr = dummy
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next, l1 = l1, l1.next
        else:
            curr.next, l2 = l2, l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next
```

- **Time:** O(n log n), **Space:** O(log n) recursion stack

---

## 5. Code Walkthrough

**Input:** `4→2→1→3`

- Split: `4→2` and `1→3`
- Sort left: split `4` and `2` → merge → `2→4`
- Sort right: split `1` and `3` → merge → `1→3`
- Merge `2→4` and `1→3` → `1→2→3→4`

**Output:** `1→2→3→4`
