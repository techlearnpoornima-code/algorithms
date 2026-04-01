# Intersection of Two Linked Lists

## 1. Problem Statement
Given heads of two linked lists, return the node where they **intersect**. Return `null` if no intersection.

- **Input:** `headA`, `headB` (ListNode)
- **Output:** Intersection node or None

---

## 2. Example
```
A: a1 → a2 ↘
              c1 → c2 → c3
B:      b1 ↗

Output: c1
```

---

## 3. Approach (Two Pointers)

**Key Idea:**
- Walk both pointers through both lists: when one reaches the end, redirect it to the other list's head.
- If they intersect, they'll meet at the intersection after at most `m+n` steps.
- If they don't intersect, both reach `None` simultaneously.

```python
def getIntersectionNode(headA, headB):
    a, b = headA, headB
    while a != b:
        a = a.next if a else headB
        b = b.next if b else headA
    return a
```

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

If list A has length 5, list B has length 4, intersection at node c1 (2 nodes from end):

- Pointer A travels 5 steps, then continues from headB
- Pointer B travels 4 steps, then continues from headA
- Both meet at c1 after m+n total steps

**Output:** Intersection node
