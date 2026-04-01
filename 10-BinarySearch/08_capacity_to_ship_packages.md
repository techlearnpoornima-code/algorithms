# Capacity to Ship Packages Within D Days

## 1. Problem Statement
Given `weights` of packages and `days`, find the **minimum weight capacity** of a ship so that all packages can be shipped within `days` days (packages must be shipped in order, no splitting).

---

## 2. Example
```
Input:  weights=[1,2,3,4,5,6,7,8,9,10], days=5
Output: 15
```

---

## 3. Approach (Binary Search on Answer)

**Key Idea:**
- The answer lies between `max(weights)` (min possible: must fit largest) and `sum(weights)` (max: ship all in one day).
- Binary search on capacity; check if it's feasible within `days`.

```python
def shipWithinDays(weights, days):
    def canShip(capacity):
        current_load = 0
        days_needed = 1
        for w in weights:
            if current_load + w > capacity:
                days_needed += 1
                current_load = 0
            current_load += w
        return days_needed <= days

    left, right = max(weights), sum(weights)
    while left < right:
        mid = (left + right) // 2
        if canShip(mid):
            right = mid
        else:
            left = mid + 1

    return left
```

- **Time Complexity:** O(n log S) — S = sum - max
- **Space Complexity:** O(1)
