# Serialize and Deserialize Binary Tree

## 1. Problem Statement
Design an algorithm to **serialize** (tree → string) and **deserialize** (string → tree) a binary tree.

---

## 2. Example
```
Input tree:   1
             / \
            2   3
               / \
              4   5

Serialized: "1,2,null,null,3,4,null,null,5,null,null"
Deserialized: same tree
```

---

## 3. Approach (Preorder DFS)

```python
class Codec:
    def serialize(self, root):
        result = []
        def dfs(node):
            if not node:
                result.append('null')
                return
            result.append(str(node.val))
            dfs(node.left)
            dfs(node.right)
        dfs(root)
        return ','.join(result)

    def deserialize(self, data):
        vals = iter(data.split(','))

        def dfs():
            val = next(vals)
            if val == 'null':
                return None
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node

        return dfs()
```

- **Time Complexity:** O(n) for both
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Serialize:** preorder DFS — root, left subtree, right subtree, nulls included.

**Deserialize:** consume values in same preorder — create node, then recurse for left and right children.
