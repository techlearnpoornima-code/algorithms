# Longest Consecutive Sequence (Hashing)

## 1. Problem Statement
Given an unsorted array, find the longest consecutive sequence. Uses hashing for O(n).

> See full solution with walkthrough in `01-Arrays/22_longest_consecutive_sequence.md`.

The key hashing insight: store all numbers in a set, then only start counting from sequence beginnings (where `num-1` is absent).

```python
def longestConsecutive(nums):
    num_set = set(nums)
    best = 0
    for num in num_set:
        if num - 1 not in num_set:
            length = 1
            while num + length in num_set:
                length += 1
            best = max(best, length)
    return best
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)
