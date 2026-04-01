# Best Time to Buy and Sell Stock

## 1. Problem Statement
Given an array `prices` where `prices[i]` is the price of a stock on day `i`, find the **maximum profit** you can achieve by buying on one day and selling on a later day. If no profit is possible, return `0`.

- **Input:** `prices` (integer array)
- **Output:** Maximum profit (integer)

---

## 2. Example
```
Input:  prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy on day 2 (price=1), sell on day 5 (price=6). Profit = 6 - 1 = 5
```

---

## 3. Brute Force Approach

**Logic:**
- Try every pair (buy day, sell day) where sell day > buy day.
- Track the maximum profit found.

```python
def maxProfit_brute(prices):
    max_profit = 0
    n = len(prices)
    for i in range(n):
        for j in range(i + 1, n):
            profit = prices[j] - prices[i]
            max_profit = max(max_profit, profit)
    return max_profit
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 4. Optimized Approach (Single Pass)

**Key Idea:**
- Track the minimum price seen so far (`min_price`).
- At each day, calculate profit if we sold today: `prices[i] - min_price`.
- Update `max_profit` accordingly.

```python
def maxProfit(prices):
    min_price = float('inf')
    max_profit = 0

    for price in prices:
        if price < min_price:
            min_price = price
        else:
            max_profit = max(max_profit, price - min_price)

    return max_profit
```

- **Time Complexity:** O(n) — single pass
- **Space Complexity:** O(1)

---

## 5. Code Walkthrough

**Input:** `prices = [7, 1, 5, 3, 6, 4]`

| Day | Price | min_price | profit today | max_profit |
|-----|-------|-----------|--------------|------------|
| 0   | 7     | 7         | 0            | 0          |
| 1   | 1     | 1         | 0            | 0          |
| 2   | 5     | 1         | 4            | 4          |
| 3   | 3     | 1         | 2            | 4          |
| 4   | 6     | 1         | 5            | 5          |
| 5   | 4     | 1         | 3            | 5          |

**Output:** `5`
