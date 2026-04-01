# Replace Words

## 1. Problem Statement
Given a dictionary of roots and a sentence, replace each word in the sentence with its shortest root from the dictionary. If no root, leave unchanged.

---

## 2. Example
```
Input:  dictionary=["cat","bat","rat"], sentence="the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

---

## 3. Approach (Trie)

```python
def replaceWords(dictionary, sentence):
    # Build Trie
    trie = {}
    for root in dictionary:
        node = trie
        for c in root:
            node = node.setdefault(c, {})
        node['$'] = root

    def find_root(word):
        node = trie
        for c in word:
            if c not in node:
                return word
            node = node[c]
            if '$' in node:
                return node['$']  # found shortest root
        return word

    return ' '.join(find_root(word) for word in sentence.split())
```

- **Time Complexity:** O(total chars in dict + sentence)
- **Space Complexity:** O(total chars in dict)
