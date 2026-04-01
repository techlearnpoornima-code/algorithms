# Top K Frequent Elements

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the `k` **most frequent elements**.

- **Input:** `nums` (integer array), `k` (integer)
- **Output:** List of k most frequent elements (any order)

---

## 2. Example
```
Input:  nums = [1,1,1,2,2,3], k = 2
Output: [1, 2]

Input:  nums = [1], k = 1
Output: [1]
```

---

## 3. Brute Force Approach

```python
def topKFrequent_brute(nums, k):
    from collections import Counter
    count = Counter(nums)
    return [x for x, _ in count.most_common(k)]
```

- **Time Complexity:** O(n log n) — sorting
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Bucket Sort)

**Key Idea:**
- Count frequencies with a hashmap.
- Use bucket sort: create `n+1` buckets where `bucket[i]` holds all numbers with frequency `i`.
- Collect from the highest-frequency bucket downward until we have k elements.

```python
def topKFrequent(nums, k):
    count = {}
    for num in nums:
        count[num] = count.get(num, 0) + 1

    # Buckets indexed by frequency
    buckets = [[] for _ in range(len(nums) + 1)]
    for num, freq in count.items():
        buckets[freq].append(num)

    result = []
    for freq in range(len(buckets) - 1, 0, -1):
        for num in buckets[freq]:
            result.append(num)
            if len(result) == k:
                return result

    return result
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `nums = [1,1,1,2,2,3]`, `k = 2`

- count: `{1:3, 2:2, 3:1}`
- buckets: `[[], [3], [2], [1], [], [], []]`
- Iterate from freq=6 down:
  - freq=3: bucket=[1] → result=[1], len=1
  - freq=2: bucket=[2] → result=[1,2], len=2 == k → return

**Output:** `[1, 2]`
