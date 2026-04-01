# 4Sum II

## 1. Problem Statement
Given four integer arrays `A`, `B`, `C`, `D` each of length `n`, return the number of tuples `(i,j,k,l)` such that `A[i] + B[j] + C[k] + D[l] == 0`.

- **Input:** Four integer arrays
- **Output:** Count of valid tuples

---

## 2. Example
```
Input:  A=[1,2], B=[-2,-1], C=[-1,2], D=[0,2]
Output: 2
```

---

## 3. Approach (HashMap — Split into Two Pairs)

**Key Idea:**
- Compute all pairwise sums of A+B, store in a hashmap with frequencies.
- For each pair C[k]+D[l], check if `-(C[k]+D[l])` exists in the map.

```python
def fourSumCount(A, B, C, D):
    ab_sums = {}
    for a in A:
        for b in B:
            ab_sums[a+b] = ab_sums.get(a+b, 0) + 1

    count = 0
    for c in C:
        for d in D:
            count += ab_sums.get(-(c+d), 0)

    return count
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n²)

---

## 5. Code Walkthrough

**Input:** A=[1,2], B=[-2,-1], C=[-1,2], D=[0,2]

AB sums: {-1:1, 0:1, 1:1} (1-2=-1, 1-1=0, 2-2=0→freq2, 2-1=1)
Actually: {-1:1, 0:2, 1:1}

For C=-1,D=0: need 1 → ab_sums[1]=1 → count+=1
For C=-1,D=2: need -1 → ab_sums[-1]=1 → count+=1

**Output:** `2`
