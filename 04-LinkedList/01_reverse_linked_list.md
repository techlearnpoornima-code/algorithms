# Reverse Linked List

## 1. Problem Statement
Given the head of a singly linked list, reverse the list and return the reversed list's head.

- **Input:** `head` (ListNode)
- **Output:** Head of reversed linked list

---

## 2. Example
```
Input:  1 → 2 → 3 → 4 → 5 → None
Output: 5 → 4 → 3 → 2 → 1 → None
```

---

## 3. Brute Force Approach (Using Stack)

```python
def reverseList_brute(head):
    stack = []
    curr = head
    while curr:
        stack.append(curr.val)
        curr = curr.next

    curr = head
    while curr:
        curr.val = stack.pop()
        curr = curr.next
    return head
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Iterative)

**Key Idea:**
- Walk through the list maintaining three pointers: `prev`, `curr`, `next_node`.
- At each step, reverse the arrow: point `curr.next` to `prev`.

```python
def reverseList(head):
    prev = None
    curr = head

    while curr:
        next_node = curr.next  # save next
        curr.next = prev       # reverse arrow
        prev = curr            # move prev forward
        curr = next_node       # move curr forward

    return prev  # prev is now the new head
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 4b. Recursive Approach

```python
def reverseList_recursive(head):
    if not head or not head.next:
        return head
    new_head = reverseList_recursive(head.next)
    head.next.next = head  # reverse the link
    head.next = None
    return new_head
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) — call stack

---

## 5. Code Walkthrough

**Input:** `1 → 2 → 3 → None`

| prev | curr | next_node | action         |
|------|------|-----------|----------------|
| None | 1    | 2         | 1.next = None  |
| 1    | 2    | 3         | 2.next = 1     |
| 2    | 3    | None      | 3.next = 2     |
| 3    | None | —         | loop ends      |

return `prev = 3`

**Output:** `3 → 2 → 1 → None`
