# Palindrome Pairs

## 1. Problem Statement
Given a list of unique words, return all pairs `[i, j]` such that `words[i] + words[j]` is a palindrome.

---

## 2. Example
```
Input:  words = ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]]
```

---

## 3. Approach (HashMap + Palindrome Check)

**Key Idea:**
- For each word, consider all splits: check if the prefix is a palindrome and the reverse of the suffix is in the map (and vice versa).

```python
def palindromePairs(words):
    word_map = {word: i for i, word in enumerate(words)}
    result = []

    def is_palindrome(s):
        return s == s[::-1]

    for i, word in enumerate(words):
        for j in range(len(word) + 1):
            prefix, suffix = word[:j], word[j:]

            # Case 1: prefix is palindrome, look for reverse of suffix
            if is_palindrome(prefix):
                rev_suffix = suffix[::-1]
                if rev_suffix in word_map and word_map[rev_suffix] != i:
                    result.append([word_map[rev_suffix], i])

            # Case 2: suffix is palindrome, look for reverse of prefix
            if j != len(word) and is_palindrome(suffix):
                rev_prefix = prefix[::-1]
                if rev_prefix in word_map and word_map[rev_prefix] != i:
                    result.append([i, word_map[rev_prefix]])

    return result
```

- **Time Complexity:** O(n × k²) — k = average word length
- **Space Complexity:** O(n × k)
