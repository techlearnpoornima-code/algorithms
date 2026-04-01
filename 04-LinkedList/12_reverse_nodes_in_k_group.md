# Reverse Nodes in K-Group

## 1. Problem Statement
Given a linked list, reverse nodes in groups of `k`. If remaining nodes < k, leave them as is.

- **Input:** `head` (ListNode), `k` (integer)
- **Output:** Modified head

---

## 2. Example
```
Input:  1→2→3→4→5, k=2
Output: 2→1→4→3→5

Input:  1→2→3→4→5, k=3
Output: 3→2→1→4→5
```

---

## 3. Approach (Iterative Group Reversal)

```python
def reverseKGroup(head, k):
    def reverse(start, end):
        prev, curr = None, start
        while curr != end:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        return prev

    def get_kth(node, k):
        while node and k > 0:
            node = node.next
            k -= 1
        return node

    dummy = ListNode(0)
    dummy.next = head
    group_prev = dummy

    while True:
        kth = get_kth(group_prev, k)
        if not kth:
            break
        group_next = kth.next

        prev_group_end = group_prev.next
        group_prev.next = reverse(group_prev.next, group_next)
        prev_group_end.next = group_next
        group_prev = prev_group_end

    return dummy.next
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4→5`, k=2

- Group 1: reverse [1,2] → 2→1, connect to rest
- Group 2: reverse [3,4] → 4→3, connect to rest
- Node 5 remaining < k → leave as is

**Output:** `2→1→4→3→5`
