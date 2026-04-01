# Remove Duplicates from Sorted List

## 1. Problem Statement
Given the head of a sorted linked list, delete all **duplicates** such that each element appears only once.

- **Input:** `head` (ListNode, sorted)
- **Output:** Head of deduplicated list

---

## 2. Example
```
Input:  1 → 1 → 2 → 3 → 3
Output: 1 → 2 → 3
```

---

## 3. Approach

```python
def deleteDuplicates(head):
    curr = head
    while curr and curr.next:
        if curr.val == curr.next.val:
            curr.next = curr.next.next  # skip duplicate
        else:
            curr = curr.next
    return head
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `1 → 1 → 2 → 3 → 3`

- curr=1: 1==1 → skip → 1→2→3→3
- curr=1: 1≠2 → move
- curr=2: 2≠3 → move
- curr=3: 3==3 → skip → 1→2→3

**Output:** `1 → 2 → 3`
