# Palindrome Linked List

## 1. Problem Statement
Given the head of a singly linked list, return `true` if it is a **palindrome**.

- **Input:** `head` (ListNode)
- **Output:** Boolean

---

## 2. Example
```
Input:  1 → 2 → 2 → 1
Output: true

Input:  1 → 2
Output: false
```

---

## 3. Brute Force

```python
def isPalindrome_brute(head):
    vals = []
    while head:
        vals.append(head.val)
        head = head.next
    return vals == vals[::-1]
```
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Reverse Second Half)

**Key Idea:**
- Find the midpoint using slow/fast pointers.
- Reverse the second half in place.
- Compare first and second halves.

```python
def isPalindrome(head):
    # Find middle
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    # Reverse second half
    prev = None
    while slow:
        nxt = slow.next
        slow.next = prev
        prev = slow
        slow = nxt

    # Compare
    left, right = head, prev
    while right:
        if left.val != right.val:
            return False
        left = left.next
        right = right.next
    return True
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1 → 2 → 2 → 1`

- Mid: slow=2 (second), fast=None
- Reverse second half: `1 → 2 → None`
- Compare: 1==1, 2==2 → True

**Output:** `True`
