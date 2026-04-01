# Time Based Key-Value Store

## 1. Problem Statement
Design a time-based key-value store:
- `set(key, value, timestamp)`: Store key-value pair at given timestamp.
- `get(key, timestamp)`: Return the value with the largest timestamp ≤ given timestamp. Return "" if none.

---

## 2. Example
```
set("foo","bar",1)
get("foo",1)  → "bar"
get("foo",3)  → "bar"
set("foo","bar2",4)
get("foo",4)  → "bar2"
get("foo",5)  → "bar2"
```

---

## 3. Approach (HashMap + Binary Search)

```python
import bisect
from collections import defaultdict

class TimeMap:
    def __init__(self):
        self.store = defaultdict(list)  # key → [(timestamp, value)]

    def set(self, key, value, timestamp):
        self.store[key].append((timestamp, value))

    def get(self, key, timestamp):
        if key not in self.store:
            return ""
        entries = self.store[key]
        # Find rightmost timestamp <= given timestamp
        lo, hi = 0, len(entries) - 1
        result = ""
        while lo <= hi:
            mid = (lo + hi) // 2
            if entries[mid][0] <= timestamp:
                result = entries[mid][1]
                lo = mid + 1
            else:
                hi = mid - 1
        return result
```

- **set:** O(1), **get:** O(log n), **Space:** O(n)
