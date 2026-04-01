# LRU Cache

## 1. Problem Statement
Design a data structure that follows the **Least Recently Used (LRU) cache** eviction policy. Implement `LRUCache(capacity)`, `get(key)`, and `put(key, value)`. Both operations must run in **O(1)** average time.

- `get(key)`: Return value if key exists, else -1. Mark as recently used.
- `put(key, value)`: Insert/update key-value. If capacity is exceeded, evict the LRU item.

---

## 2. Example
```
LRUCache(2)
put(1, 1)  → cache: {1:1}
put(2, 2)  → cache: {1:1, 2:2}
get(1)     → 1   (1 is now most recent)
put(3, 3)  → evict 2 (LRU), cache: {1:1, 3:3}
get(2)     → -1  (not found)
get(3)     → 3
```

---

## 3. Brute Force Approach

```python
def get_brute(self, key):
    if key in self.cache:
        # move to end to mark as recently used
        val = self.cache.pop(key)
        self.cache[key] = val
        return val
    return -1
```
Using Python's `OrderedDict` — simpler but same idea.

- **Time Complexity:** O(1) amortized (OrderedDict)
- **Space Complexity:** O(capacity)

---

## 4. Optimized Approach (HashMap + Doubly Linked List)

**Key Idea:**
- HashMap gives O(1) key lookup.
- Doubly Linked List maintains order: most recent at tail, LRU at head.
- On `get`/`put`: move accessed node to tail.
- On eviction: remove node at head.

```python
class Node:
    def __init__(self, key=0, val=0):
        self.key, self.val = key, val
        self.prev = self.next = None

class LRUCache:
    def __init__(self, capacity):
        self.cap = capacity
        self.cache = {}  # key -> Node
        # Dummy head (LRU end) and tail (MRU end)
        self.head = Node()
        self.tail = Node()
        self.head.next = self.tail
        self.tail.prev = self.head

    def _remove(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev

    def _add_to_tail(self, node):
        node.prev = self.tail.prev
        node.next = self.tail
        self.tail.prev.next = node
        self.tail.prev = node

    def get(self, key):
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add_to_tail(node)
            return node.val
        return -1

    def put(self, key, value):
        if key in self.cache:
            self._remove(self.cache[key])
        node = Node(key, value)
        self.cache[key] = node
        self._add_to_tail(node)
        if len(self.cache) > self.cap:
            lru = self.head.next
            self._remove(lru)
            del self.cache[lru.key]
```

- **Time Complexity:** O(1) for both get and put
- **Space Complexity:** O(capacity)

---

## 5. Code Walkthrough

**LRUCache(2), put(1,1), put(2,2), get(1), put(3,3)**

```
After put(1,1): head ↔ [1] ↔ tail
After put(2,2): head ↔ [1] ↔ [2] ↔ tail
After get(1):   head ↔ [2] ↔ [1] ↔ tail  (1 moved to tail)
After put(3,3): capacity exceeded → remove head.next = [2]
                head ↔ [1] ↔ [3] ↔ tail
```

get(2) → -1 (evicted), get(3) → 3
