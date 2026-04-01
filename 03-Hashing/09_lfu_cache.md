# LFU Cache

## 1. Problem Statement
Design a **Least Frequently Used (LFU)** cache. Implement `get(key)` and `put(key, value)`. When capacity is exceeded, evict the least frequently used key. Ties are broken by least recently used.

- All operations must be **O(1)**.

---

## 2. Example
```
LFUCache(2)
put(1,1), put(2,2)
get(1)     → 1   (freq[1]=2, freq[2]=1)
put(3,3)   → evict key 2 (lowest freq)
get(2)     → -1
get(3)     → 3
```

---

## 3. Approach (HashMap + Doubly Linked List per Frequency)

**Key Idea:**
- `key_val`: key → value
- `key_freq`: key → frequency
- `freq_keys`: frequency → OrderedDict of keys (maintains insertion order for LRU tiebreaker)
- `min_freq`: tracks the current minimum frequency

```python
from collections import defaultdict, OrderedDict

class LFUCache:
    def __init__(self, capacity):
        self.cap = capacity
        self.key_val = {}
        self.key_freq = {}
        self.freq_keys = defaultdict(OrderedDict)
        self.min_freq = 0

    def _update(self, key):
        freq = self.key_freq[key]
        del self.freq_keys[freq][key]
        if not self.freq_keys[freq] and freq == self.min_freq:
            self.min_freq += 1
        self.key_freq[key] = freq + 1
        self.freq_keys[freq + 1][key] = True

    def get(self, key):
        if key not in self.key_val:
            return -1
        self._update(key)
        return self.key_val[key]

    def put(self, key, value):
        if self.cap <= 0:
            return
        if key in self.key_val:
            self.key_val[key] = value
            self._update(key)
        else:
            if len(self.key_val) >= self.cap:
                evict_key, _ = self.freq_keys[self.min_freq].popitem(last=False)
                del self.key_val[evict_key]
                del self.key_freq[evict_key]
            self.key_val[key] = value
            self.key_freq[key] = 1
            self.freq_keys[1][key] = True
            self.min_freq = 1
```

- **Time Complexity:** O(1) for both get and put
- **Space Complexity:** O(capacity)
