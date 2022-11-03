---
weight: 256
title: "256 Paint House"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

There is a row of `n` houses, where each house can be painted one of three colors: red, blue, or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an `n x 3` cost matrix `costs`.

- For example, `costs[0][0]` is the cost of painting house `0` with the color red; `costs[1][2]` is the cost of painting house 1 with color green, and so on...

Return _the minimum cost to paint all houses_.

**Example 1:**
```
Input: costs = [[17,2,17],[16,16,5],[14,3,19]]
Output: 10
Explanation: Paint house 0 into blue, paint house 1 into green,
paint house 2 into blue.
Minimum cost: 2 + 5 + 3 = 10.
```
**Example 2:**
```
Input: costs = [[7,6,2]]
Output: 2
```

**Constraints:**
- `costs.length == n`
- `costs[i].length == 3`
- `1 <= n <= 100`
- `1 <= costs[i][j] <= 20`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minCost(self, costs: List[List[int]]) -> int:
        r, b, g = costs[0]
        for i in range(1, len(costs)):
            cur_r, cur_b, cur_g = costs[i]
            r, b, g = (
                min(g, b) + cur_r,
                min(r, g) + cur_b,
                min(r, b) + cur_g,
            )
        return min(r, b, g)
{{< / highlight >}}
</div>
</div>
