# Asteroid Collision

## 1. Problem Statement
Given an array `asteroids` where positive = moving right, negative = moving left. When they collide, the smaller one explodes (equal size → both explode). Find the state after all collisions.

---

## 2. Example
```
Input:  asteroids = [5,10,-5]   → [5,10]  (-5 hits 10, explodes)
Input:  asteroids = [8,-8]      → []      (equal, both explode)
Input:  asteroids = [10,2,-5]   → [10]    (-5 hits 2→explodes, then -5 vs 10→explodes)
```

---

## 3. Approach (Stack)

**Key Idea:**
- Push asteroids onto stack.
- Collision only happens when top of stack is positive and current is negative.
- Compare sizes and pop accordingly.

```python
def asteroidCollision(asteroids):
    stack = []

    for a in asteroids:
        while stack and a < 0 < stack[-1]:
            if stack[-1] < -a:
                stack.pop()    # stack top destroyed, continue
                continue
            elif stack[-1] == -a:
                stack.pop()    # both destroyed
            break              # current asteroid destroyed
        else:
            stack.append(a)    # no collision, push

    return stack
```

- **Time:** O(n), **Space:** O(n)

---

## 5. Code Walkthrough

**Input:** `[10, 2, -5]`

| a  | stack before | action              | stack after |
|----|-------------|---------------------|-------------|
| 10 | []          | push                | [10]        |
| 2  | [10]        | push                | [10,2]      |
| -5 | [10,2]      | 2 < 5 → pop 2, continue; 10 > 5 → break | [10] |

**Output:** `[10]`
