# Sum Root to Leaf Numbers

## 1. Problem Statement
Given a binary tree where each node has a digit (0-9), each root-to-leaf path represents a number. Return the **sum of all root-to-leaf numbers**.

---

## 2. Example
```
Input:      1
           / \
          2   3

Paths: 12 + 13 = 25
Output: 25

Input:      4
           / \
          9   0
         / \
        5   1

Paths: 495 + 491 + 40 = 1026
Output: 1026
```

---

## 3. Approach (DFS)

```python
def sumNumbers(root):
    def dfs(node, current):
        if not node: return 0
        current = current * 10 + node.val
        if not node.left and not node.right:
            return current   # leaf: return formed number
        return dfs(node.left, current) + dfs(node.right, current)

    return dfs(root, 0)
```

- **Time:** O(n), **Space:** O(h)

---

## 5. Code Walkthrough

**Input:** Tree [4,9,0,5,1]

- dfs(4,0): current=4
  - dfs(9,4): current=49
    - dfs(5,49): current=495, leaf → return 495
    - dfs(1,49): current=491, leaf → return 491
  - dfs(0,4): current=40, leaf → return 40

Total = 495+491+40 = **1026**

**Output:** `1026`
