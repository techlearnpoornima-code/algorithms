# Copy List with Random Pointer

## 1. Problem Statement
A linked list where each node has `next` and `random` pointers (random can point to any node or null). Return a **deep copy**.

---

## 2. Example
```
Input:  [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: Deep copy of the same structure
```

---

## 3. Brute Force (HashMap)

```python
def copyRandomList_map(head):
    if not head: return None
    node_map = {}
    curr = head
    while curr:
        node_map[curr] = Node(curr.val)
        curr = curr.next
    curr = head
    while curr:
        if curr.next:
            node_map[curr].next = node_map[curr.next]
        if curr.random:
            node_map[curr].random = node_map[curr.random]
        curr = curr.next
    return node_map[head]
```

- **Time:** O(n), **Space:** O(n)

---

## 4. Optimized Approach (Interleaving — O(1) Space)

**Key Idea:**
- Step 1: Insert cloned nodes between each original and its next: `A→A'→B→B'→C→C'`
- Step 2: Set random pointers: `clone.random = original.random.next`
- Step 3: Separate the two lists.

```python
def copyRandomList(head):
    if not head: return None

    # Step 1: Interleave clones
    curr = head
    while curr:
        clone = Node(curr.val)
        clone.next = curr.next
        curr.next = clone
        curr = clone.next

    # Step 2: Set random pointers
    curr = head
    while curr:
        if curr.random:
            curr.next.random = curr.random.next
        curr = curr.next.next

    # Step 3: Separate lists
    dummy = Node(0)
    clone_curr = dummy
    curr = head
    while curr:
        clone_curr.next = curr.next
        curr.next = curr.next.next
        clone_curr = clone_curr.next
        curr = curr.next

    return dummy.next
```

- **Time:** O(n), **Space:** O(1)
