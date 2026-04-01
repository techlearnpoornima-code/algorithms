# Stream of Characters

## 1. Problem Statement
Design a class `StreamChecker` that checks if any word from a given list is a suffix of the characters streamed so far.

- `StreamChecker(words)`: Initialize with a word list.
- `query(letter)`: Returns true if any word in the list is a suffix of the stream.

---

## 2. Example
```
StreamChecker(["cd","f","kl"])
query('a') → false
query('b') → false
query('c') → false
query('d') → true   ("cd" is suffix of "abcd")
query('e') → false
query('f') → true   ("f" is suffix of "abcdef")
```

---

## 3. Approach (Reversed Trie)

**Key Idea:**
- Insert all words **reversed** into a Trie.
- For each query, prepend the new character to a buffer and search the Trie with the reversed buffer.
- This way we check if any word is a suffix of the stream.

```python
class StreamChecker:
    def __init__(self, words):
        self.trie = {}
        self.stream = []

        # Insert reversed words into trie
        for word in words:
            node = self.trie
            for c in reversed(word):
                node = node.setdefault(c, {})
            node['$'] = True

        self.max_len = max(len(w) for w in words)

    def query(self, letter):
        self.stream.append(letter)
        node = self.trie

        # Search reversed stream in trie
        for c in reversed(self.stream[-self.max_len:]):
            if c not in node:
                return False
            node = node[c]
            if '$' in node:
                return True

        return False
```

- **query:** O(max_word_len), **Space:** O(total characters in words)

---

## 5. Code Walkthrough

words=["cd","f"], reversed: ["dc","f"]

Trie: {'d':{'c':{'$':True}}, 'f':{'$':True}}

stream=['a','b','c','d']:
- query('d'): check reversed stream "dcba" in trie → 'd'→'c'→'$' found! → **True**
