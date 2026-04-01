# Task Scheduler

## 1. Problem Statement
Given tasks (letters) and cooldown `n`, find the **minimum intervals** needed to execute all tasks. Same tasks must be `n` intervals apart. CPU can be idle.

---

## 2. Example
```
Input:  tasks=["A","A","A","B","B","B"], n=2
Output: 8
Explanation: A→B→idle→A→B→idle→A→B
```

---

## 3. Approach (Greedy with Max Heap)

**Key Idea:**
- Always schedule the most frequent remaining task next.
- If no task is available (cooldown), idle.
- Use a max heap for frequencies and a queue for cooled-down tasks.

```python
import heapq
from collections import Counter, deque

def leastInterval(tasks, n):
    counts = Counter(tasks)
    heap = [-cnt for cnt in counts.values()]
    heapq.heapify(heap)

    queue = deque()  # (negative_count, available_at_time)
    time = 0

    while heap or queue:
        time += 1
        if heap:
            cnt = heapq.heappop(heap) + 1  # use one task
            if cnt:
                queue.append((cnt, time + n))
        if queue and queue[0][1] == time:
            heapq.heappush(heap, queue.popleft()[0])

    return time
```

- **Time Complexity:** O(T log T) — T = unique task types
- **Space Complexity:** O(T)

---

## 4. Math Approach (O(n))

```python
def leastInterval_math(tasks, n):
    counts = Counter(tasks)
    max_count = max(counts.values())
    max_count_tasks = sum(1 for v in counts.values() if v == max_count)
    return max(len(tasks), (max_count - 1) * (n + 1) + max_count_tasks)
```
