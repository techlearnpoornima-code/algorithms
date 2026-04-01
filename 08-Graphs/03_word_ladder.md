# Word Ladder

## 1. Problem Statement
Given a `beginWord`, an `endWord`, and a `wordList`, find the **length of the shortest transformation sequence** from beginWord to endWord, where each step changes exactly one letter and each intermediate word must be in wordList. Return 0 if no path exists.

- **Input:** `beginWord`, `endWord` (strings), `wordList` (list of strings)
- **Output:** Length of shortest path, or 0

---

## 2. Example
```
Input:  beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Path:   hit → hot → dot → dog → cog
```

---

## 3. Brute Force (DFS)

```python
def ladderLength_brute(beginWord, endWord, wordList):
    word_set = set(wordList)
    def dfs(word, visited, steps):
        if word == endWord:
            return steps
        min_steps = float('inf')
        for w in word_set:
            if w not in visited and sum(a != b for a, b in zip(word, w)) == 1:
                visited.add(w)
                result = dfs(w, visited, steps + 1)
                min_steps = min(min_steps, result)
                visited.remove(w)
        return min_steps
    res = dfs(beginWord, {beginWord}, 1)
    return res if res != float('inf') else 0
```

- **Time Complexity:** Very slow — exponential
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (BFS)

**Key Idea:**
- BFS guarantees the shortest path.
- At each step, try changing each character of the current word to any letter a-z.
- If the new word is in the word set, add it to the queue and remove from the set (avoid revisits).

```python
from collections import deque

def ladderLength(beginWord, endWord, wordList):
    word_set = set(wordList)
    if endWord not in word_set:
        return 0

    queue = deque([(beginWord, 1)])

    while queue:
        word, length = queue.popleft()
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                new_word = word[:i] + c + word[i+1:]
                if new_word == endWord:
                    return length + 1
                if new_word in word_set:
                    word_set.remove(new_word)
                    queue.append((new_word, length + 1))

    return 0
```

- **Time Complexity:** O(M² × N) — M = word length, N = wordList size
- **Space Complexity:** O(M² × N)

---

## 5. Code Walkthrough

**Input:** `"hit" → "cog"`, wordList=["hot","dot","dog","lot","log","cog"]

BFS levels:
- Level 1: "hit"
- Level 2: "hot" (h→h, i→o, t→t)
- Level 3: "dot", "lot"
- Level 4: "dog", "log"
- Level 5: "cog" ← found! return 5

**Output:** `5`
