# Pascal's Triangle

## 1. Problem Statement
Given an integer `numRows`, return the first `numRows` of Pascal's triangle.

---

## 2. Example
```
Input:  numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

---

## 3. Approach

```python
def generate(numRows):
    triangle = [[1]]
    for i in range(1, numRows):
        prev = triangle[-1]
        row = [1] + [prev[j] + prev[j+1] for j in range(len(prev)-1)] + [1]
        triangle.append(row)
    return triangle
```

- **Time:** O(numRows²), **Space:** O(numRows²)
