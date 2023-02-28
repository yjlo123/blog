---
weight: 2398
title: "2398 Maximum Number of Robots Within Budget"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_sliding_window", "lc_queue"]
---

You have `n` robots. You are given two **0-indexed** integer arrays, `chargeTimes` and `runningCosts`, both of length `n`. The <code>i<sup>th</sup></code> robot costs `chargeTimes[i]` units to charge and costs `runningCosts[i]` units to run. You are also given an integer `budget`.

The total cost of running `k` chosen robots is equal to `max(chargeTimes) + k * sum(runningCosts)`, where `max(chargeTimes)` is the largest charge cost among the `k` robots and `sum(runningCosts)` is the sum of running costs among the `k` robots.

Return *the **maximum** number of **consecutive** robots you can run such that the total cost **does not** exceed `budget`*.


**Example 1:**
```
Input: chargeTimes = [3,6,1,3,4], runningCosts = [2,1,3,4,5], budget = 25
Output: 3
Explanation: 
It is possible to run all individual and consecutive pairs of robots within budget.
To obtain answer 3, consider the first 3 robots.
The total cost will be max(3,6,1) + 3 * sum(2,1,3) = 6 + 3 * 6 = 24
which is less than 25.
It can be shown that it is not possible to run more than 3 consecutive robots
within budget, so we return 3.
```
**Example 2:**
```
Input: chargeTimes = [11,12,19], runningCosts = [10,8,7], budget = 19
Output: 0
Explanation: No robot can be run that does not exceed the budget, so we return 0.
```

**Constraints:**
- `chargeTimes.length == runningCosts.length == n`
- <code>1 <= n <= 5 * 10<sup>4</sup></code>
- <code>1 <= chargeTimes[i], runningCosts[i] <= 10<sup>5</sup></code>
- <code>1 <= budget <= 10<sup>15</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maximumRobots(
        self,
        chargeTimes: List[int],
        runningCosts: List[int],
        budget: int
    ) -> int:
        n = len(chargeTimes)
        max_q = deque()
        max_len = 0
        current_sum = 0
        l, r = 0, -1

        for cc, rc in zip(chargeTimes, runningCosts):
            r += 1
            # update max queue
            while max_q and max_q[-1] < cc:
                max_q.pop()
            max_q.append(cc)
            current_sum += rc
            # contract window left
            while l < r and max_q and max_q[0] + (r-l+1) * current_sum > budget:
                if chargeTimes[l] == max_q[0]:
                    max_q.popleft()
                current_sum -= runningCosts[l]
                l += 1
            # check if it's a valid window
            if max_q and max_q[0] + (r-l+1) * current_sum <= budget:
                max_len = max(max_len, r - l + 1)

        return max_len
{{< / highlight >}}
</div>
</div>
