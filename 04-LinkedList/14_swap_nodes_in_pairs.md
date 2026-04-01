# Swap Nodes in Pairs

## 1. Problem Statement
Given a linked list, swap every two **adjacent** nodes and return its head. Must not modify node values.

---

## 2. Example
```
Input:  1→2→3→4
Output: 2→1→4→3
```

---

## 3. Approach (Iterative)

```python
def swapPairs(head):
    dummy = ListNode(0)
    dummy.next = head
    prev = dummy

    while prev.next and prev.next.next:
        first = prev.next
        second = prev.next.next

        # Swap
        first.next = second.next
        second.next = first
        prev.next = second

        prev = first  # move to end of swapped pair

    return dummy.next
```

- **Time:** O(n), **Space:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4`

| prev | first | second | after swap |
|------|-------|--------|------------|
| dummy| 1     | 2      | dummy→2→1→3→4 |
| 1    | 3     | 4      | 1→4→3→None |

**Output:** `2→1→4→3`
