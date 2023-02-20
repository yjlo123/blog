---
weight: 1383
title: "1383 Maximum Performance of a Team"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_heap", "lc_sorting", "lc_greedy"]
---

You are given two integers `n` and `k` and two integer arrays `speed` and `efficiency` both of length `n`. There are `n` engineers numbered from `1` to `n`. `speed[i]` and `efficiency[i]` represent the speed and efficiency of the <code>i<sup>th</sup></code> engineer respectively.

Choose **at most** `k` different engineers out of the `n` engineers to form a team with the maximum **performance**.

The performance of a team is the sum of their engineers' speeds multiplied by the minimum efficiency among their engineers.

Return the maximum performance of this team. Since the answer can be a huge number, return it modulo <code>10<sup>9</sup> + 7</code>.

**Example 1:**
```
Input: n = 6, speed = [2,10,3,1,5,8], efficiency = [5,4,3,9,7,2], k = 2
Output: 60
Explanation: 
We have the maximum performance of the team by selecting 
engineer 2 (with speed=10 and efficiency=4) and
engineer 5 (with speed=5 and efficiency=7).
That is, performance = (10 + 5) * min(4, 7) = 60.
```
**Example 2:**
```
Input: n = 6, speed = [2,10,3,1,5,8], efficiency = [5,4,3,9,7,2], k = 3
Output: 68
Explanation:
This is the same example as the first but k = 3. We can select engineer 1,
engineer 2 and engineer 5 to get the maximum performance of the team.
That is, performance = (2 + 10 + 5) * min(5, 4, 7) = 68.
```
**Example 3:**
```
Input: n = 6, speed = [2,10,3,1,5,8], efficiency = [5,4,3,9,7,2], k = 4
Output: 72
```

**Constraints:**
- <code>1 <= k <= n <= 10<sup>5</sup></code>
- `speed.length == n`
- `efficiency.length == n`
- <code>1 <= speed[i] <= 10<sup>5</sup></code>
- <code>1 <= efficiency[i] <= 10<sup>8</sup></code>

> 1. Keep track of the engineers by their efficiency in decreasing order.  
> 2. Starting from one engineer, to build a team, it suffices to bring K-1 more engineers who have higher efficiencies as well as high speeds.


<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxPerformance(
        self,
        n: int,
        speed: List[int],
        efficiency: List[int],
        k: int
    ) -> int:
        MOD = 10 ** 9 + 7
        engineers = list(zip(speed, efficiency))
        engineers.sort(key=lambda x: -x[1])
        speed_heap = []
        speed_sum = 0
        max_perf = -1
        for s, e in engineers:
            if len(speed_heap) > k - 1:
                speed_sum -= heapq.heappop(speed_heap)
            heapq.heappush(speed_heap, s)
            speed_sum += s
            max_perf = max(max_perf, e * speed_sum)
        return max_perf % MOD
{{< / highlight >}}
</div>
</div>
