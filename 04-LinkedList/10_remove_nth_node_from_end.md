# Remove Nth Node From End of List

## 1. Problem Statement
Given the head of a linked list, remove the **n-th node from the end** and return its head. Do it in one pass.

- **Input:** `head` (ListNode), `n` (integer)
- **Output:** Modified head

---

## 2. Example
```
Input:  1→2→3→4→5, n=2
Output: 1→2→3→5
```

---

## 3. Approach (Two Pointers, One Pass)

**Key Idea:**
- Use `fast` and `slow` pointers. Move `fast` n+1 steps ahead.
- Then move both until `fast` is None — `slow` is just before the node to remove.

```python
def removeNthFromEnd(head, n):
    dummy = ListNode(0)
    dummy.next = head
    fast = slow = dummy

    for _ in range(n + 1):
        fast = fast.next

    while fast:
        fast = fast.next
        slow = slow.next

    slow.next = slow.next.next
    return dummy.next
```

- **Time Complexity:** O(L) — one pass
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4→5`, n=2

- Move fast 3 steps ahead: fast=3
- Move both until fast=None: slow=3, fast=None
- slow.next = slow.next.next → skip node 4

**Output:** `1→2→3→5`
