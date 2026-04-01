# Coin Change

## 1. Problem Statement
Given an array of coin denominations `coins` and a total `amount`, return the **fewest number of coins** needed to make up that amount. Return `-1` if it cannot be achieved.

- **Input:** `coins` (integer array), `amount` (integer)
- **Output:** Minimum coins needed, or -1

---

## 2. Example
```
Input:  coins = [1, 2, 5], amount = 11
Output: 3  (5 + 5 + 1)

Input:  coins = [2], amount = 3
Output: -1
```

---

## 3. Brute Force Approach (Recursion)

```python
def coinChange_brute(coins, amount):
    def dp(rem):
        if rem < 0: return -1
        if rem == 0: return 0
        best = float('inf')
        for coin in coins:
            res = dp(rem - coin)
            if res != -1:
                best = min(best, res + 1)
        return best if best != float('inf') else -1
    return dp(amount)
```

- **Time Complexity:** O(S^n) — exponential
- **Space Complexity:** O(S)

---

## 4. Optimized Approach (Bottom-Up DP)

**Key Idea:**
- Build dp array where `dp[i]` = minimum coins to make amount `i`.
- For each amount from 1 to `amount`, try every coin: `dp[i] = min(dp[i], dp[i - coin] + 1)`.
- Initialize with `float('inf')` (impossible), `dp[0] = 0`.

```python
def coinChange(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0  # 0 coins needed for amount 0

    for i in range(1, amount + 1):
        for coin in coins:
            if coin <= i:
                dp[i] = min(dp[i], dp[i - coin] + 1)

    return dp[amount] if dp[amount] != float('inf') else -1
```

- **Time Complexity:** O(S × n) — S = amount, n = coins count
- **Space Complexity:** O(S)

---

## 5. Code Walkthrough

**Input:** `coins = [1, 2, 5]`, `amount = 11`

Key dp values:
- dp[0]=0, dp[1]=1, dp[2]=1, dp[3]=2, dp[4]=2
- dp[5]=1 (one coin of 5)
- dp[6]=2, ..., dp[10]=2
- dp[11]: coin=5 → dp[6]+1=3, coin=2 → dp[9]+1=3, coin=1 → dp[10]+1=3 → **3**

**Output:** `3`
