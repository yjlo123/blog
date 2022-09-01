---
weight: 322
title: "322 Coin Change"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount._ If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```
**Example 2:**
```
Input: coins = [2], amount = 3
Output: -1
```
**Example 3:**
```
Input: coins = [1], amount = 0
Output: 0
```

**Constraints:**
- `1 <= coins.length <= 12`
- <code>1 <= coins[i] <= 2<sup>31</sup> - 1</code>
- <code>0 <= amount <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [amount+1] * (amount + 1)
        dp[0] = 0
        
        for i in range(amount+1):
            for c in coins:
                if i >= c and dp[i-c] + 1 < dp[i]:
                    dp[i] = dp[i-c] + 1
        return dp[amount] if dp[amount] < amount+1 else -1
{{< / highlight >}}
</div>
</div>
