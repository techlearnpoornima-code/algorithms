# Merge Two Sorted Lists

## 1. Problem Statement
Given the heads of two sorted linked lists `list1` and `list2`, merge them into a single sorted list and return its head.

- **Input:** `list1`, `list2` (ListNode heads)
- **Output:** Head of merged sorted list

---

## 2. Example
```
Input:  list1 = 1→2→4, list2 = 1→3→4
Output: 1→1→2→3→4→4
```

---

## 3. Brute Force Approach

```python
def mergeTwoLists_brute(list1, list2):
    vals = []
    while list1:
        vals.append(list1.val)
        list1 = list1.next
    while list2:
        vals.append(list2.val)
        list2 = list2.next

    dummy = ListNode(0)
    curr = dummy
    for v in sorted(vals):
        curr.next = ListNode(v)
        curr = curr.next
    return dummy.next
```

- **Time Complexity:** O((m+n) log(m+n))
- **Space Complexity:** O(m+n)

---

## 4. Optimized Approach (Two Pointers with Dummy Node)

**Key Idea:**
- Use a dummy head node to simplify edge cases.
- Compare the current nodes of both lists; attach the smaller one to the result.
- When one list is exhausted, attach the rest of the other.

```python
def mergeTwoLists(list1, list2):
    dummy = ListNode(0)
    curr = dummy

    while list1 and list2:
        if list1.val <= list2.val:
            curr.next = list1
            list1 = list1.next
        else:
            curr.next = list2
            list2 = list2.next
        curr = curr.next

    curr.next = list1 if list1 else list2  # attach remaining
    return dummy.next
```

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1→2→4`, `1→3→4`

| l1 val | l2 val | pick | result so far |
|--------|--------|------|---------------|
| 1      | 1      | l1=1 | dummy→1       |
| 2      | 1      | l2=1 | →1→1          |
| 2      | 3      | l1=2 | →1→1→2        |
| 4      | 3      | l2=3 | →1→1→2→3      |
| 4      | 4      | l1=4 | →1→1→2→3→4    |
| None   | 4      | attach l2 | →1→1→2→3→4→4 |

**Output:** `1→1→2→3→4→4`
