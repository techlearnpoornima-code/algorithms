# Word Ladder

## 1. Problem Statement
Find the **shortest transformation sequence** from `beginWord` to `endWord` where each step changes exactly one letter and every intermediate word must be in `wordList`.

> See full solution in `08-Graphs/03_word_ladder.md`.

This duplicate file serves as a reference. The BFS approach guarantees shortest path:

```python
from collections import deque

def ladderLength(beginWord, endWord, wordList):
    word_set = set(wordList)
    if endWord not in word_set: return 0
    queue = deque([(beginWord, 1)])
    while queue:
        word, length = queue.popleft()
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                new_word = word[:i] + c + word[i+1:]
                if new_word == endWord: return length + 1
                if new_word in word_set:
                    word_set.remove(new_word)
                    queue.append((new_word, length + 1))
    return 0
```
- **Time:** O(M² × N), **Space:** O(M² × N)
