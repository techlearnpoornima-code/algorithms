# Map Sum Pairs

## 1. Problem Statement
Design a `MapSum` class:
- `insert(key, val)`: Insert key-val pair. If key exists, override.
- `sum(prefix)`: Return sum of all values whose keys start with `prefix`.

---

## 2. Example
```
insert("apple", 3), sum("ap") → 3
insert("app", 2),   sum("ap") → 5
```

---

## 3. Approach (Trie with Values)

```python
class MapSum:
    def __init__(self):
        self.trie = {}
        self.vals = {}

    def insert(self, key, val):
        delta = val - self.vals.get(key, 0)
        self.vals[key] = val
        node = self.trie
        for c in key:
            node = node.setdefault(c, {'_sum': 0})
            node['_sum'] += delta

    def sum(self, prefix):
        node = self.trie
        for c in prefix:
            if c not in node:
                return 0
            node = node[c]
        return node.get('_sum', 0)
```

- **insert:** O(k), **sum:** O(k) — k = key/prefix length
