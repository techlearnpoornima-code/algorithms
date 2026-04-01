# Substring with Concatenation of All Words

## 1. Problem Statement
Given a string `s` and array `words` of same-length words, return all starting indices of substrings that are a concatenation of all words (in any order, no gaps).

- **Input:** `s` (string), `words` (string array)
- **Output:** List of starting indices

---

## 2. Example
```
Input:  s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
```

---

## 3. Approach (Sliding Window + HashMap)

```python
def findSubstring(s, words):
    from collections import Counter
    if not s or not words:
        return []

    word_len = len(words[0])
    word_count = len(words)
    total_len = word_len * word_count
    word_freq = Counter(words)
    result = []

    for i in range(len(s) - total_len + 1):
        seen = {}
        j = 0
        while j < word_count:
            word = s[i + j * word_len : i + (j+1) * word_len]
            if word in word_freq:
                seen[word] = seen.get(word, 0) + 1
                if seen[word] > word_freq[word]:
                    break
            else:
                break
            j += 1
        if j == word_count:
            result.append(i)

    return result
```

- **Time Complexity:** O(n × m × w) — n=len(s), m=words count, w=word length
- **Space Complexity:** O(m)

---

## 5. Code Walkthrough

**Input:** `s = "barfoothefoobarman"`, `words = ["foo","bar"]`

- i=0: "bar"✅ "foo"✅ → append 0
- i=9: "foo"✅ "bar"✅ → append 9

**Output:** `[0, 9]`
