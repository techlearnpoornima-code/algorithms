# Move Zeroes (Two Pointers)

## 1. Problem Statement
Move all 0s to the end of the array while maintaining relative order of non-zero elements.

> See full solution in `01-Arrays/05_move_zeroes.md`.

---

## 2. Two Pointer Pattern

Use a slow pointer (`write_pos`) and fast pointer iterating through the array:

```python
def moveZeroes(nums):
    write_pos = 0
    for num in nums:
        if num != 0:
            nums[write_pos] = num
            write_pos += 1
    while write_pos < len(nums):
        nums[write_pos] = 0
        write_pos += 1
```

- **Time:** O(n), **Space:** O(1)
