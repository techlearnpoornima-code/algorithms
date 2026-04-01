# Odd Even Linked List

## 1. Problem Statement
Given a singly linked list, group all nodes at **odd indices** first, then **even indices**. Do it in O(1) space and O(n) time. Index starts at 1.

---

## 2. Example
```
Input:  1→2→3→4→5
Output: 1→3→5→2→4
```

---

## 3. Approach

**Key Idea:** Maintain two pointers `odd` and `even`. Move odd to skip over even nodes and vice versa. Connect odd tail to even head at the end.

```python
def oddEvenList(head):
    if not head:
        return head

    odd = head
    even = head.next
    even_head = even

    while even and even.next:
        odd.next = even.next   # odd skips over even
        odd = odd.next
        even.next = odd.next   # even skips over next odd
        even = even.next

    odd.next = even_head       # connect odd tail to even list
    return head
```

- **Time:** O(n), **Space:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4→5`

| step | odd | even | list state |
|------|-----|------|------------|
| 1    | 3   | 4    | 1→3→5, 2→4 |
| 2    | 5   | None | done       |

Connect: 5→2

**Output:** `1→3→5→2→4`
