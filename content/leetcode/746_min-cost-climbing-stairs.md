---
weight: 746
title: "746 Min Cost Climbing Stairs"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_dp"]
---

You are given an integer array `cost` where `cost[i]` is the cost of <code>i<sup>th</sup></code> step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return _the minimum cost to reach the top of the floor_.

**Example 1:**
```
Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.
```
**Example 2:**
```
Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.
```

**Constraints:**
- `2 <= cost.length <= 1000`
- `0 <= cost[i] <= 999`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        p1, p2 = cost[0], cost[1]
        for i in range(2, len(cost)):
            p1, p2 = p2, min(p1, p2) + cost[i]
        return min(p1, p2)
{{< / highlight >}}
</div>
</div>
