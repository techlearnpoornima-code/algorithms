# Design Add and Search Words Data Structure

## 1. Problem Statement
Design a data structure with:
- `addWord(word)`: adds a word.
- `search(word)`: returns true if word is in the structure. `.` can match any letter.

---

## 2. Example
```
addWord("bad"), addWord("dad"), addWord("mad")
search("pad") → false
search("bad") → true
search(".ad") → true
search("b..") → true
```

---

## 3. Approach (Trie + DFS for Wildcards)

```python
class WordDictionary:
    def __init__(self):
        self.root = {}

    def addWord(self, word):
        node = self.root
        for c in word:
            node = node.setdefault(c, {})
        node['$'] = True

    def search(self, word):
        def dfs(node, i):
            if i == len(word):
                return '$' in node
            c = word[i]
            if c == '.':
                return any(dfs(child, i+1) for key, child in node.items() if key != '$')
            if c not in node:
                return False
            return dfs(node[c], i+1)

        return dfs(self.root, 0)
```

- **addWord:** O(m), **search:** O(m) normal, O(26^m) worst case with all dots
- **Space:** O(total characters)

---

## 5. Code Walkthrough

search(".ad"):
- Node root, c='.' → try all children: 'b','d','m'
  - DFS from 'b', i=1: c='a' → go to 'a' node
    - DFS from 'a' node, i=2: c='d' → found! return True ✅
