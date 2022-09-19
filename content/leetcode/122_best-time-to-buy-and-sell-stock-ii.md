---
weight: 122
title: "122 Best Time to Buy and Sell Stock II"
date: 2020-10-25T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return _the **maximum** profit you can achieve_.

**Example 1:**
```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```
**Example 2:**
```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```
**Example 3:**
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
 ```

**Constraints:**

- <code>1 <= prices.length <= 3 * 10<sup>4</sup></code>
- <code>0 <= prices[i] <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        total = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                total += prices[i] - prices[i-1]
        return total
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func maxProfit(prices []int) int {
    if prices == nil || len(prices) == 0 {
        return 0
    }

    profit := 0
    for i := 0; i < len(prices)-1; i++ {
        if prices[i+1] > prices[i] {
            profit += prices[i+1] - prices[i]
        }
    }
    return profit
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode122" target="_blank">https://runtime.siwei.dev/?src=leetcode122</a>
    </div>
</div>
</div>
