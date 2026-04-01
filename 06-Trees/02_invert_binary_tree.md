# Invert Binary Tree

## 1. Problem Statement
Given the root of a binary tree, invert the tree (mirror it), and return its root.

- **Input:** `root` (TreeNode)
- **Output:** Root of inverted tree

---

## 2. Example
```
Input:          Output:
     4               4
    / \             / \
   2   7    →      7   2
  / \ / \         / \ / \
 1  3 6  9       9  6 3  1
```

---

## 3. Recursive Approach

**Key Idea:**
- Swap left and right children at each node, then recursively invert both subtrees.

```python
def invertTree(root):
    if not root:
        return None
    root.left, root.right = root.right, root.left
    invertTree(root.left)
    invertTree(root.right)
    return root
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(h) — recursion stack

---

## 4. Iterative Approach (BFS)

```python
from collections import deque

def invertTree_iterative(root):
    if not root:
        return None
    queue = deque([root])
    while queue:
        node = queue.popleft()
        node.left, node.right = node.right, node.left
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    return root
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(w) — max queue size = max width

---

## 5. Code Walkthrough

**Input:** Tree rooted at 4

- Visit 4: swap children → left=7, right=2
- Visit 7: swap children → left=9, right=6
- Visit 2: swap children → left=3, right=1
- All leaves have no children → base case

**Output:** Mirrored tree
