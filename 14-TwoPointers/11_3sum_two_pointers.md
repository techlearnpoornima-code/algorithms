# 3Sum (Two Pointers)

## 1. Problem Statement
Find all unique triplets that sum to zero.

> See full solution in `01-Arrays/13_3sum.md`.

---

## 2. Two Pointer Pattern

Sort + fix one element + two-pointer search for complement:

```python
def threeSum(nums):
    nums.sort()
    result = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i-1]: continue
        left, right = i+1, len(nums)-1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left+1]: left += 1
                while left < right and nums[right] == nums[right-1]: right -= 1
                left += 1; right -= 1
            elif total < 0: left += 1
            else: right -= 1
    return result
```

- **Time:** O(n²), **Space:** O(1)
