---
weight: 123
title: "123 Best Time to Buy and Sell Stock III"
date: 2021-03-26T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_hard"]
---

You are given an array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**
```
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```
**Example 2:**
```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later,
as you are engaging multiple transactions at the same time.
You must sell before buying again.
```
**Example 3:**
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```
**Example 4:**
```
Input: prices = [1]
Output: 0
```

**Constraints:**

- <code>1 <= prices.length <= 10<sup>5</sup></code>
- <code>0 <= prices[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        t1_cost, t2_cost = float('inf'), float('inf')
        t1_profit, t2_profit = 0, 0
        
        for p in prices:
            # max profit if only one txn is allowed
            t1_cost = min(t1_cost, p)
            t1_profit = max(t1_profit, p - t1_cost)
            # reinvest the gain in the second txn
            t2_cost = min(t2_cost, p - t1_profit)
            t2_profit = max(t2_profit, p - t2_cost)
        return t2_profit
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
// dp[k, i] = max(dp[k, i-1], prices[i] - prices[j] + dp[k-1, j-1]), j=[0..i-1]

func maxProfit(prices []int) int {
	if len(prices) == 0 {
		return 0
	}
	buy1 := prices[0]
	sell1 := 0
	buy2 := prices[0]
	sell2 := 0
	for _, p := range prices {
		buy1 = min(buy1, p)
		sell1 = max(sell1, p-buy1)
		buy2 = min(buy2, p-sell1)
		sell2 = max(sell2, p-buy2)
	}
	return sell2
}
{{< / highlight >}}
</div>
</div>
