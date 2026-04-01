# Isomorphic Strings

## 1. Problem Statement
Given two strings `s` and `t`, determine if they are **isomorphic** — characters in `s` can be replaced to get `t`, with each character mapping to exactly one character (and vice versa).

- **Input:** `s`, `t` (strings)
- **Output:** Boolean

---

## 2. Example
```
Input:  s = "egg", t = "add"
Output: true   (e→a, g→d)

Input:  s = "foo", t = "bar"
Output: false  (o maps to both 'a' and 'r')

Input:  s = "paper", t = "title"
Output: true   (p→t, a→i, e→l, r→e)
```

---

## 3. Brute Force Approach

```python
def isIsomorphic_brute(s, t):
    return len(set(zip(s, t))) == len(set(s)) == len(set(t))
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 4. Optimized Approach (Two HashMaps)

**Key Idea:**
- Use two maps: one for `s→t` mapping, one for `t→s` mapping.
- At each position, check that the mapping is consistent in both directions.

```python
def isIsomorphic(s, t):
    s_to_t = {}
    t_to_s = {}

    for cs, ct in zip(s, t):
        if cs in s_to_t and s_to_t[cs] != ct:
            return False
        if ct in t_to_s and t_to_s[ct] != cs:
            return False
        s_to_t[cs] = ct
        t_to_s[ct] = cs

    return True
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) — at most 256 ASCII character mappings

---

## 5. Code Walkthrough

**Input:** `s = "foo"`, `t = "bar"`

| cs | ct | s_to_t    | t_to_s    | Valid? |
|----|----|-----------|-----------|--------|
| f  | b  | {f:b}     | {b:f}     | ✅ |
| o  | a  | {f:b,o:a} | {b:f,a:o} | ✅ |
| o  | r  | o→a but ct=r ≠ a | — | ❌ return False |

**Output:** `False`
