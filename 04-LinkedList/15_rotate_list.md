# Rotate List

## 1. Problem Statement
Given a linked list, rotate it to the **right** by `k` places.

---

## 2. Example
```
Input:  1→2→3→4→5, k=2
Output: 4→5→1→2→3
```

---

## 3. Approach

**Key Idea:**
- Find length `n`, effective rotation = `k % n`.
- Make the list circular, then break at the right position.

```python
def rotateRight(head, k):
    if not head or not head.next or k == 0:
        return head

    # Find length and tail
    tail = head
    n = 1
    while tail.next:
        tail = tail.next
        n += 1

    k = k % n
    if k == 0:
        return head

    # Find new tail (n-k-1 steps from head)
    new_tail = head
    for _ in range(n - k - 1):
        new_tail = new_tail.next

    # Rotate
    new_head = new_tail.next
    new_tail.next = None
    tail.next = head

    return new_head
```

- **Time:** O(n), **Space:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→3→4→5`, k=2, n=5, effective k=2

- new_tail = node at index 2 (node 3)
- new_head = node 4
- tail(5).next = head(1)
- new_tail(3).next = None

**Output:** `4→5→1→2→3`
