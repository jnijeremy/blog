---
layout: post
title: Dynamic Programming
update: 2016-2-25
excerpt: <p>A collection of dynamic programming problems</p>

---

[The Maximum Subarray](https://www.hackerrank.com/challenges/maxsubarray)

Given an array, find the maximum possible sum of a contiguous subarray.

Sample Input

```
2 -1 2 3 4 -5	
```

Sample Output

```
10
// 2 -1 2 3 4
```

**Solution**

looks like dp, try define opt(i) as max result from [0,i], but doesn't work since not knowing if arr[i] is in the max contiguous subarray.  
What about assume arr[i] is in the current max result and also keep a global result?  So for arr[i], if arr[i] is positive, current max result includes arr[i] and update global max result.  If arr[i] is negative, current max result = arr[i] itself.

```python
def max_cont_subarray(arr):
	max_end_here = max_so_far = arr[0]
	for i in arr[1:]:
		max_end_here = max(max_end_here + i, i)
		max_so_far = max(max_so_far, max_end_here)
	return max_so_far	
```

---

[The Coin Change Problem](https://www.hackerrank.com/challenges/coin-change/)

How many different ways can you make change for an amount, given a list of coins?  

**Sample Input**
	
```
4 3 // N = amount to make change, M = types of coins
1 2 3
```
	
**Sample Output**
	
```
4
// (1 1 1 1), (1 1 2), (2 2), (1 3)
```
	
**Solution**
	
For each coin, we build and update the dp array.  dp[i] means the number of ways to make change for amount `i`.

```python
def getCoins(n, coins):
    dp = [1] + [0]*n
    for coin in coins:
        for i in range(n):
            if i + coin <= n:
                dp[i+coin] += dp[i]
    return dp[n]
```

---

[Stock Maximize](https://www.hackerrank.com/challenges/stockmax)

Given array of prices, output the maximum profit.  Each day, you can either buy one share, sell any number of shares that you own, or not make any transaction at all.
	
**Sample Input**
	
```
1 2 100
```
	
**Sample Output**
	
```
197
// 1 buy, 2 buy, 100 sell all
```
	
**Solution**
	
Loop back form the tail of the princes, keep track of the highest price and profit.  If arr[i] is lower than highest, buy at arr[i] and sell at highest.  If arr[i] is higher or equal then highest, update highest to arr[i], prifit doesn't change.
	
```python
def getMaxProfit(prices):
	maxPrice, maxProfit = -1, 0
	for i in range(len(prices)-1, -1, -1):
		maxPrice = max(maxPrice, prices[i]
		maxProfit += maxPrice - prices[i]
```
