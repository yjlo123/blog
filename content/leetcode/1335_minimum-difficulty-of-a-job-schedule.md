---
weight: 1335
title: "1335 Minimum Difficulty of a Job Schedule"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp"]
---

You want to schedule a list of jobs in `d` days. Jobs are dependent (i.e To work on the <code>i<sup>th</sup></code> job, you have to finish all the jobs `j` where `0 <= j < i`).

You have to finish **at least** one task every day. The difficulty of a job schedule is the sum of difficulties of each day of the d days. The difficulty of a day is the maximum difficulty of a job done on that day.

You are given an integer array `jobDifficulty` and an integer `d`. The difficulty of the <code>i<sup>th</sup></code> job is `jobDifficulty[i]`.

Return the minimum difficulty of a job schedule. If you cannot find a schedule for the jobs return `-1`.

**Example 1:**
```
Day1: 6 5 4 3 2
Day2: 1

Input: jobDifficulty = [6,5,4,3,2,1], d = 2
Output: 7
Explanation: First day you can finish the first 5 jobs, total difficulty = 6.
Second day you can finish the last job, total difficulty = 1.
The difficulty of the schedule = 6 + 1 = 7
```
**Example 2:**
```
Input: jobDifficulty = [9,9,9], d = 4
Output: -1
Explanation: If you finish a job per day you will still have a free day.
you cannot find a schedule for the given jobs.
```
**Example 3:**
```
Input: jobDifficulty = [1,1,1], d = 3
Output: 3
Explanation: The schedule is one job per day. total difficulty will be 3.
```

**Constraints:**
- `1 <= jobDifficulty.length <= 300`
- `0 <= jobDifficulty[i] <= 1000`
- `1 <= d <= 10`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    '''
    min_diff(i, d) = min_diff(j, d - 1) + max(jobDifficulty[i:j]) for all j > i
    '''
    def minDifficulty(self, jobDifficulty: List[int], d: int) -> int:
        n = len(jobDifficulty)
        if n < d:
            return -1
        max_job_remaining = jobDifficulty[:]
        for i in range(n-2, -1, -1):
            max_job_remaining[i] = max(
                max_job_remaining[i],
                max_job_remaining[i + 1]
            )
            
        cache = {}

        def min_diff(i, days_remaining):
            if (i, days_remaining) in cache:
                return cache[(i, days_remaining)]
            if days_remaining == 1:
                return max_job_remaining[i]
            res = float('inf')
            daily_max_job_diff = 0
            for j in range(i, n - days_remaining + 1):
                daily_max_job_diff = max(
                    daily_max_job_diff,
                    jobDifficulty[j]
                )
                res = min(
                    res,
                    daily_max_job_diff + min_diff(j + 1, days_remaining - 1)
                )
            cache[(i, days_remaining)] = res
            return res
        
        return min_diff(0, d)
{{< / highlight >}}
</div>
</div>
