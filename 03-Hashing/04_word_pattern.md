# Word Pattern

## 1. Problem Statement
Given a `pattern` and a string `s`, return `true` if `s` **follows the same pattern** — there is a bijection between each letter in `pattern` and each non-empty word in `s`.

- **Input:** `pattern` (string), `s` (space-separated string)
- **Output:** Boolean

---

## 2. Example
```
Input:  pattern = "abba", s = "dog cat cat dog"
Output: true

Input:  pattern = "abba", s = "dog cat cat fish"
Output: false

Input:  pattern = "aaaa", s = "dog cat cat dog"
Output: false
```

---

## 3. Brute Force

```python
def wordPattern_brute(pattern, s):
    words = s.split()
    if len(pattern) != len(words):
        return False
    return len(set(zip(pattern, words))) == len(set(pattern)) == len(set(words))
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Two HashMaps)

**Key Idea:**
- Maintain bidirectional mapping: pattern char → word AND word → pattern char.
- At each position, verify both mappings are consistent.

```python
def wordPattern(pattern, s):
    words = s.split()
    if len(pattern) != len(words):
        return False

    char_to_word = {}
    word_to_char = {}

    for ch, word in zip(pattern, words):
        if ch in char_to_word and char_to_word[ch] != word:
            return False
        if word in word_to_char and word_to_char[word] != ch:
            return False
        char_to_word[ch] = word
        word_to_char[word] = ch

    return True
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `pattern = "abba"`, `s = "dog cat cat dog"`

| ch | word | char_to_word   | word_to_char      | Valid? |
|----|------|----------------|-------------------|--------|
| a  | dog  | {a:dog}        | {dog:a}           | ✅ |
| b  | cat  | {a:dog,b:cat}  | {dog:a,cat:b}     | ✅ |
| b  | cat  | b→cat matches  | cat→b matches     | ✅ |
| a  | dog  | a→dog matches  | dog→a matches     | ✅ |

**Output:** `True`
