# Reorder List

## 1. Problem Statement
Given list `L0→L1→…→Ln`, reorder it to `L0→Ln→L1→Ln-1→L2→Ln-2→…` in place.

- **Input:** `head` (ListNode)
- **Output:** Modified in-place

---

## 2. Example
```
Input:  1→2→3→4
Output: 1→4→2→3

Input:  1→2→3→4→5
Output: 1→5→2→4→3
```

---

## 3. Approach (Find Middle + Reverse + Merge)

```python
def reorderList(head):
    if not head or not head.next:
        return

    # Step 1: Find middle
    slow, fast = head, head
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next

    # Step 2: Reverse second half
    prev, curr = None, slow.next
    slow.next = None
    while curr:
        nxt = curr.next
        curr.next = prev
        prev = curr
        curr = nxt

    # Step 3: Merge two halves
    first, second = head, prev
    while second:
        tmp1, tmp2 = first.next, second.next
        first.next = second
        second.next = tmp1
        first = tmp1
        second = tmp2
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4→5`

- Middle: node 3, second half: `4→5`
- Reversed: `5→4`
- Merge: 1→5→2→4→3

**Output:** `1→5→2→4→3`
