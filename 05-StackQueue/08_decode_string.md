# Decode String

## 1. Problem Statement
Given an encoded string like `k[encoded_string]`, return the decoded string where `encoded_string` is repeated `k` times. `k` is always a positive integer.

- **Input:** `s` (encoded string)
- **Output:** Decoded string

---

## 2. Example
```
Input:  "3[a]2[bc]"  → "aaabcbc"
Input:  "3[a2[c]]"   → "accaccacc"
```

---

## 3. Approach (Stack)

**Key Idea:**
- Use a stack to handle nesting.
- When `[` is seen: push current string and current number onto stack, reset both.
- When `]` is seen: pop count and previous string, repeat current string count times, append to previous.

```python
def decodeString(s):
    stack = []
    current_str = ""
    current_num = 0

    for char in s:
        if char.isdigit():
            current_num = current_num * 10 + int(char)
        elif char == '[':
            stack.append((current_str, current_num))
            current_str = ""
            current_num = 0
        elif char == ']':
            prev_str, num = stack.pop()
            current_str = prev_str + current_str * num
        else:
            current_str += char

    return current_str
```

- **Time Complexity:** O(output length)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `"3[a2[c]]"`

- '3' → num=3
- '[' → stack=[("",3)], reset
- 'a' → curr="a"
- '2' → num=2
- '[' → stack=[("",3),("a",2)], reset
- 'c' → curr="c"
- ']' → pop ("a",2): curr="a"+"c"*2="acc"
- ']' → pop ("",3): curr=""+"acc"*3="accaccacc"

**Output:** `"accaccacc"`
