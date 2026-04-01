# Expression Add Operators

## 1. Problem Statement
Given a string `num` and integer `target`, return all possible ways to insert `+`, `-`, or `*` between digits to make the expression equal `target`.

---

## 2. Example
```
Input:  num = "123", target = 6
Output: ["1+2+3","1*2*3"]

Input:  num = "232", target = 8
Output: ["2+3*2","2*3+2"]
```

---

## 3. Approach (Backtracking with Carry for Multiplication)

**Key Idea:**
- Track `current_eval` and `prev_operand` (for multiplication precedence).
- On `*`: subtract previous operand, multiply it, add back.

```python
def addOperators(num, target):
    result = []

    def backtrack(idx, path, eval_val, prev):
        if idx == len(num):
            if eval_val == target:
                result.append(path)
            return

        for i in range(idx, len(num)):
            curr_str = num[idx:i+1]
            if len(curr_str) > 1 and curr_str[0] == '0':
                break  # no leading zeros
            curr = int(curr_str)

            if idx == 0:
                backtrack(i+1, curr_str, curr, curr)
            else:
                backtrack(i+1, path+'+'+curr_str, eval_val+curr, curr)
                backtrack(i+1, path+'-'+curr_str, eval_val-curr, -curr)
                backtrack(i+1, path+'*'+curr_str, eval_val-prev+prev*curr, prev*curr)

    backtrack(0, "", 0, 0)
    return result
```

- **Time Complexity:** O(4^n × n)
- **Space Complexity:** O(n)
