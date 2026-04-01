# Add Two Numbers

## 1. Problem Statement
Two non-empty linked lists represent two non-negative integers stored in **reverse order**. Add the two numbers and return the sum as a linked list (also in reverse order).

- **Input:** `l1`, `l2` (ListNode)
- **Output:** Head of result linked list

---

## 2. Example
```
Input:  (2→4→3) + (5→6→4)
        342 + 465 = 807
Output: 7 → 0 → 8
```

---

## 3. Approach (Simulate Addition)

```python
def addTwoNumbers(l1, l2):
    dummy = ListNode(0)
    curr = dummy
    carry = 0

    while l1 or l2 or carry:
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0

        total = val1 + val2 + carry
        carry = total // 10
        curr.next = ListNode(total % 10)
        curr = curr.next

        if l1: l1 = l1.next
        if l2: l2 = l2.next

    return dummy.next
```

- **Time Complexity:** O(max(m,n))
- **Space Complexity:** O(max(m,n))

---

## 5. Code Walkthrough

**Input:** `2→4→3` and `5→6→4`

| l1 | l2 | carry | sum | digit | carry_out |
|----|----|----|-----|-------|-----------|
| 2  | 5  | 0  | 7   | 7     | 0         |
| 4  | 6  | 0  | 10  | 0     | 1         |
| 3  | 4  | 1  | 8   | 8     | 0         |

**Output:** `7 → 0 → 8`
