# Linked List Cycle

## 1. Problem Statement
Given the head of a linked list, determine if the list has a **cycle** (a node's `next` pointer points to a previous node). Return `true` if there is a cycle.

- **Input:** `head` (ListNode)
- **Output:** Boolean

---

## 2. Example
```
Input:  3 → 2 → 0 → -4 → (back to 2)
Output: true

Input:  1 → 2 → None
Output: false
```

---

## 3. Brute Force Approach (HashSet)

```python
def hasCycle_brute(head):
    seen = set()
    curr = head
    while curr:
        if id(curr) in seen:
            return True
        seen.add(id(curr))
        curr = curr.next
    return False
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Floyd's Cycle Detection)

**Key Idea:**
- Use two pointers: `slow` moves 1 step, `fast` moves 2 steps.
- If there's a cycle, fast will eventually "lap" slow and they'll meet.
- If fast reaches None, there's no cycle.

```python
def hasCycle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True

    return False
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `3 → 2 → 0 → -4 → (back to node 2)`

| step | slow | fast |
|------|------|------|
| 0    | 3    | 3    |
| 1    | 2    | 0    |
| 2    | 0    | 2    |
| 3    | -4   | -4   |
| 4    | 2    | 2    | ← slow == fast → cycle! |

**Output:** `True`
