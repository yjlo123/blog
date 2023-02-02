---
weight: 539
title: "539 Minimum Time Difference"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

Given a list of 24-hour clock time points in **"HH:MM"** format, return *the minimum minutes difference between any two time-points in the list*.

**Example 1:**
```
Input: timePoints = ["23:59","00:00"]
Output: 1
```
**Example 2:**
```
Input: timePoints = ["00:00","23:59","00:00"]
Output: 0
```

**Constraints:**
- <code>2 <= timePoints.length <= 2 * 10<sup>4</sup></code>
- `timePoints[i]` is in the format **"HH:MM"**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findMinDifference(self, timePoints: List[str]) -> int:
        ts = []
        for t in timePoints:
            h, m = map(int, t.split(':'))
            ts.append(h * 60 + m)
        ts.sort()
        min_diff = math.inf
        for i in range(1, len(ts)):
            min_diff = min(min_diff, ts[i] - ts[i - 1])
        min_diff = min(min_diff, ts[0] + 1440 - ts[-1])
        return min_diff
{{< / highlight >}}
</div>
</div>
