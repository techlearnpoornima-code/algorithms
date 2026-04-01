# Implement Trie (Prefix Tree)

## 1. Problem Statement
Implement a **Trie** data structure with three operations:
- `insert(word)`: Insert a word into the trie.
- `search(word)`: Return true if the word exists in the trie.
- `startsWith(prefix)`: Return true if any word in the trie starts with the given prefix.

---

## 2. Example
```
Trie trie = new Trie();
trie.insert("apple")
trie.search("apple")    → true
trie.search("app")      → false
trie.startsWith("app")  → true
trie.insert("app")
trie.search("app")      → true
```

---

## 3. Brute Force (HashSet)

```python
class Trie_brute:
    def __init__(self):
        self.words = set()

    def insert(self, word):
        self.words.add(word)

    def search(self, word):
        return word in self.words

    def startsWith(self, prefix):
        return any(w.startswith(prefix) for w in self.words)
```

- **startsWith:** O(n × m) where n=words, m=prefix length

---

## 4. Optimized Approach (Trie Node)

**Key Idea:**
- Each node has 26 children (one per letter) and an `is_end` flag.
- `insert`: walk/create nodes character by character, mark last as end.
- `search`: walk nodes; return True only if last node has `is_end=True`.
- `startsWith`: walk nodes; return True if all characters are found.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end

    def startsWith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

- **Time Complexity:** O(m) per operation, m = word/prefix length
- **Space Complexity:** O(total characters inserted)

---

## 5. Code Walkthrough

**Operations:** insert("apple"), search("app"), startsWith("app")

After insert("apple"):
```
root → 'a' → 'p' → 'p' → 'l' → 'e'(is_end=True)
```

search("app"):
- Traverse a→p→p: all nodes exist, but `is_end` of last 'p' = False → **False**

startsWith("app"):
- Traverse a→p→p: all nodes exist → **True**
