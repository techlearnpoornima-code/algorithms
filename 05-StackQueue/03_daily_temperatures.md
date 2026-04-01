# Daily Temperatures

## 1. Problem Statement
Given an array `temperatures` of daily temperatures, return an array `answer` where `answer[i]` is the number of days you have to wait after day `i` to get a **warmer temperature**. If no future day is warmer, `answer[i] = 0`.

- **Input:** `temperatures` (integer array)
- **Output:** `answer` array of wait days

---

## 2. Example
```
Input:  temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

---

## 3. Brute Force Approach

```python
def dailyTemperatures_brute(temperatures):
    n = len(temperatures)
    answer = [0] * n
    for i in range(n):
        for j in range(i + 1, n):
            if temperatures[j] > temperatures[i]:
                answer[i] = j - i
                break
    return answer
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Monotonic Stack)

**Key Idea:**
- Use a stack that stores **indices** of temperatures in decreasing order.
- When the current temperature is warmer than the temperature at the stack's top index, pop and record the wait days.
- This is a classic **monotonic decreasing stack** pattern.

```python
def dailyTemperatures(temperatures):
    n = len(temperatures)
    answer = [0] * n
    stack = []  # stores indices

    for i, temp in enumerate(temperatures):
        while stack and temperatures[stack[-1]] < temp:
            prev_idx = stack.pop()
            answer[prev_idx] = i - prev_idx
        stack.append(i)

    return answer
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 5. Code Walkthrough

**Input:** `[73, 74, 75, 71, 69, 72, 76, 73]`

| i | temp | stack (before) | popped indices | answer updates |
|---|------|----------------|----------------|----------------|
| 0 | 73   | []             | —              | push 0         |
| 1 | 74   | [0]            | 0 (73<74)      | ans[0]=1       |
| 2 | 75   | [1]            | 1 (74<75)      | ans[1]=1       |
| 3 | 71   | [2]            | —              | push 3         |
| 4 | 69   | [2,3]          | —              | push 4         |
| 5 | 72   | [2,3,4]        | 4 (69<72), 3 (71<72) | ans[4]=1, ans[3]=2 |
| 6 | 76   | [2,5]          | 5 (72<76), 2 (75<76) | ans[5]=1, ans[2]=4 |
| 7 | 73   | [6]            | —              | push 7         |

**Output:** `[1,1,4,2,1,1,0,0]`
