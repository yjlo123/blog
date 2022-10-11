---
weight: 739
title: "739 Daily Temperatures"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack"]
---

Given an array of integers `temperatures` represents the daily temperatures, return _an array `answer` such that `answer[i]` is the number of days you have to wait after the <code>i<sup>th</sup></code> day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.


**Example 1:**
```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```
**Example 2:**
```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```
**Example 3:**
```
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

**Constraints:**
- <code>1 <= temperatures.length <= 10<sup>5</sup></code>
- `30 <= temperatures[i] <= 100`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        res = [0] * n
        stack = []
        for cur_day, cur_temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < cur_temp:
                prev_day = stack.pop()
                res[prev_day] = cur_day - prev_day
            stack.append(cur_day)
        return res
{{< / highlight >}}
</div>
</div>
