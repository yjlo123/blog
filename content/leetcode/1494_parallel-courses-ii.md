---
weight: 1494
title: "1494 Parallel Courses II"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp", "lc_bit"]
---

You are given an integer `n`, which indicates that there are `n` courses labeled from `1` to `n`. You are also given an array `relations` where <code>relations[i] = [prevCourse<sub>i</sub>, nextCourse<sub>i</sub>]</code>, representing a prerequisite relationship between course prevCoursei and course nextCoursei: course <code>prevCourse<sub>i</sub></code> has to be taken before course <code>nextCourse<sub>i</sub></code>. Also, you are given the integer `k`.

In one semester, you can take **at most** `k` courses as long as you have taken all the prerequisites in the **previous** semesters for the courses you are taking.

Return *the **minimum** number of semesters needed to take all courses*. The testcases will be generated such that it is possible to take every course.

**Example 1:**
```
2
 \
  -> 1 -> 4
 /
3

Input: n = 4, relations = [[2,1],[3,1],[1,4]], k = 2
Output: 3
Explanation: The figure above represents the given graph.
In the first semester, you can take courses 2 and 3.
In the second semester, you can take course 1.
In the third semester, you can take course 4.
```
**Example 2:**
```
2
 \
3 -> 1 -> 5
 /
4

Input: n = 5, relations = [[2,1],[3,1],[4,1],[1,5]], k = 2
Output: 4
Explanation: The figure above represents the given graph.
In the first semester, you can only take courses 2 and 3 
  since you cannot take more than two per semester.
In the second semester, you can take course 4.
In the third semester, you can take course 1.
In the fourth semester, you can take course 5.
```

**Constraints:**
- `1 <= n <= 15`
- `1 <= k <= n`
- `0 <= relations.length <= n * (n-1) / 2`
- `relations[i].length == 2`
- <code>1 <= prevCourse<sub>i</sub>, nextCourse<sub>i</sub> <= n</code>
- <code>prevCourse<sub>i</sub> != nextCourse<sub>i</sub></code>
- All the pairs <code>[prevCourse<sub>i</sub>, nextCourse<sub>i</sub>]</code> are unique.
- The given graph is a directed acyclic graph.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minNumberOfSemesters(self, n: int, relations: List[List[int]], k: int) -> int:
        if k == 1:
            return n
        if len(relations) == 0:
            return math.ceil(n / k)

        prev = [0] * n
        for r in relations:
            prev[r[1] - 1] |= (1 << (r[0] - 1))

        num_of_states = 1 << n
        f = [n] * num_of_states # min steps for each state
        f[0] = 0
        for state in range(num_of_states):
            # first iteration, state = 0
            # all courses with no pre will be picked up
            if f[state] == n or f[state] == n - 1:
                continue
            available = [
                i for i in range(n)
                if (
                    state & (1 << i) == 0 # (i) is not studied yet
                    and state & prev[i] == prev[i] # all prerequisites of (i) satisfied
                )
            ]
            for combi in itertools.combinations(available, min(len(available), k)):
                new_state = state
                for c in combi:
                    new_state |= (1 << c)
                f[new_state] = min(f[new_state], f[state] + 1)
        return f[(1 << n) - 1]
{{< / highlight >}}
</div>
</div>
