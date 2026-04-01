# Word Search II (Trie + Backtracking)

## 1. Problem Statement
Given an `m x n` board of characters and a list of strings `words`, return all words found in the board. Words must be constructed from sequentially adjacent cells (horizontally or vertically), and each cell may only be used once per word.

- **Input:** `board` (2D char array), `words` (string list)
- **Output:** List of found words

---

## 2. Example
```
Input:
  board = [["o","a","a","n"],
           ["e","t","a","e"],
           ["i","h","k","r"],
           ["i","f","l","v"]]
  words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]
```

---

## 3. Brute Force

Run DFS (Word Search I) for each word — O(words × m × n × 4^L).

---

## 4. Optimized Approach (Trie + DFS)

**Key Idea:**
- Build a Trie from all words.
- DFS from every cell; at each step follow the Trie path.
- When a word is found (`is_end=True`), add to results and continue DFS.
- Mark cells visited during DFS to avoid reuse.

```python
def findWords(board, words):
    # Build Trie
    trie = {}
    for word in words:
        node = trie
        for c in word:
            node = node.setdefault(c, {})
        node['$'] = word  # mark end of word

    rows, cols = len(board), len(board[0])
    result = []

    def dfs(node, r, c):
        char = board[r][c]
        if char not in node:
            return
        next_node = node[char]
        if '$' in next_node:
            result.append(next_node['$'])
            del next_node['$']  # avoid duplicates

        board[r][c] = '#'  # mark visited
        for dr, dc in [(0,1),(0,-1),(1,0),(-1,0)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and board[nr][nc] != '#':
                dfs(next_node, nr, nc)
        board[r][c] = char  # restore

    for r in range(rows):
        for c in range(cols):
            dfs(trie, r, c)

    return result
```

- **Time Complexity:** O(m × n × 4^L × W) — L=max word len, W=words
- **Space Complexity:** O(total Trie nodes)

---

## 5. Code Walkthrough

**For word "eat":**
- Start DFS from 'e' at (1,0): e→a not adjacent... try (1,3): e→a→t → found! ✅
- Add "eat" to results

**For word "oath":**
- Find 'o' at (0,0): o→a→t→h found via adjacent path ✅
