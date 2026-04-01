# Sqrt(x)

## 1. Problem Statement
Given a non-negative integer `x`, return the **integer square root** (floor value).

---

## 2. Example
```
Input: x=4  → 2
Input: x=8  → 2  (floor of 2.828)
```

---

## 3. Approach (Binary Search)

```python
def mySqrt(x):
    if x < 2:
        return x
    left, right = 1, x // 2
    while left <= right:
        mid = (left + right) // 2
        if mid * mid == x:
            return mid
        elif mid * mid < x:
            left = mid + 1
        else:
            right = mid - 1
    return right  # right is the floor sqrt
```

- **Time:** O(log x), **Space:** O(1)
