# Fruit Into Baskets

## 1. Problem Statement
You have two baskets that can each hold one type of fruit. Given a fruit array, find the **length of the longest subarray** with at most 2 distinct fruit types.

---

## 2. Example
```
Input:  fruits = [1,2,1]
Output: 3

Input:  fruits = [0,1,2,2]
Output: 3  ([1,2,2])

Input:  fruits = [1,2,3,2,2]
Output: 4  ([2,3,2,2])
```

---

## 3. Approach (Sliding Window)

```python
def totalFruit(fruits):
    basket = {}
    left = 0
    max_len = 0

    for right, fruit in enumerate(fruits):
        basket[fruit] = basket.get(fruit, 0) + 1

        while len(basket) > 2:
            basket[fruits[left]] -= 1
            if basket[fruits[left]] == 0:
                del basket[fruits[left]]
            left += 1

        max_len = max(max_len, right - left + 1)

    return max_len
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) — at most 3 keys

---

## 5. Code Walkthrough

**Input:** `[1,2,3,2,2]`

| right | fruit | basket       | left | window |
|-------|-------|--------------|------|--------|
| 0     | 1     | {1:1}        | 0    | 1      |
| 1     | 2     | {1:1,2:1}    | 0    | 2      |
| 2     | 3     | {1:1,2:1,3:1}| 0→1  | 2      |
|       |       | {2:1,3:1}    | 1    |        |
| 3     | 2     | {2:2,3:1}    | 1    | 3      |
| 4     | 2     | {2:3,3:1}    | 1    | 4      |

**Output:** `4`
