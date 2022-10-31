---
weight: 70
title: "70 Climbing Stairs"
date: 2021-09-21T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_dp"]
---

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

**Constraints:**
- 1 <= n <= 45

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 3:
            return n
        prev_2 = 1
        prev_1 = 2
        for i in range(2, n):
            current = prev_2 + prev_1
            prev_2 = prev_1
            prev_1 = current
        return prev_1
{{< / highlight >}}
</div>
</div>
