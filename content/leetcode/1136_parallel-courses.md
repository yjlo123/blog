---
weight: 1136
title: "1136 Parallel Courses"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bfs"]
---

You are given an integer `n`, which indicates that there are `n` courses labeled from `1` to `n`. You are also given an array `relations` where <code>relations[i] = [prevCourse<sub>i</sub>, nextCourse<sub>i</sub>]</code>, representing a prerequisite relationship between course <code>prevCourse<sub>i</sub></code> and course <code>nextCourse<sub>i</sub></code>: course <code>prevCourse<sub>i</sub></code> has to be taken before course <code>nextCourse<sub>i</sub></code>.

In one semester, you can take **any number** of courses as long as you have taken all the prerequisites in the **previous** semester for the courses you are taking.

Return _the **minimum** number of semesters needed to take all courses_. If there is no way to take all the courses, return `-1`.


**Example 1:**
```
1   2
 \ /
  v
  3

Input: n = 3, relations = [[1,3],[2,3]]
Output: 2
Explanation: The figure above represents the given graph.
In the first semester, you can take courses 1 and 2.
In the second semester, you can take course 3.
```
**Example 2:**
```
1 --> 2
^    /
 \  v
   3

Input: n = 3, relations = [[1,2],[2,3],[3,1]]
Output: -1
Explanation: No course can be studied because they are prerequisites of each other.
```

**Constraints:**
- `1 <= n <= 5000`
- `1 <= relations.length <= 5000`
- `relations[i].length == 2`
- <code>1 <= prevCourse<sub>i</sub>, nextCourse<sub>i</sub> <= n</code>
- <code>prevCourse<sub>i</sub> != nextCourse<sub>i</sub></code>
- All the pairs <code>[prevCourse<sub>i</sub>, nextCourse<sub>i</sub>]</code> are **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minimumSemesters(self, n: int, relations: List[List[int]]) -> int:
        graph = defaultdict(list)
        indegree = defaultdict(int)
        for pre, course in relations:
            graph[pre].append(course)
            indegree[course] += 1
        
        queue = [i for i in range(1, n+1) if i not in indegree]
        count = 0
        while queue:
            count += 1
            temp = []
            for course in queue:
                for next_course in graph[course]:
                    indegree[next_course] -= 1
                    if indegree[next_course] == 0:
                        temp.append(next_course)
                        del indegree[next_course]
            queue = temp
        
        return count if not indegree else -1
{{< / highlight >}}
</div>
</div>
