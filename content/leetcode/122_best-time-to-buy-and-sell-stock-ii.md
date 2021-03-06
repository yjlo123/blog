---
weight: 122
title: "122 Best Time to Buy and Sell Stock II"
date: 2020-10-25T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Say you have an array `prices` for which the _i<sup>th</sup>_ element is the price of a given stock on day _i_.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

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

- 1 <= prices.length <= 3 * 10<sup>4</sup>
- 0 <= prices[i] <= 10<sup>4</sup>

<div class="tabs"></div>
<div class="tab-content">
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
