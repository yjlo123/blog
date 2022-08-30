---
weight: 210
title: "210 Course Schedule II"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "graph"]
---

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course bi first if you want to take course <code>a<sub>i</sub></code>.

- For example, the pair `[0, 1]`, indicates that to take course 0 you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses._ If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. 
So the correct course order is [0,1].
```
**Example 2:**
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you
should have finished both courses 1 and 2. Both courses 1 and 2 should be
taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```
**Example 3:**
```
Input: numCourses = 1, prerequisites = []
Output: [0]
```

**Constraints:**
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
- `prerequisites[i].length == 2`
- <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
- <code>a<sub>i</sub> != b<sub>i</sub></code>
- All the pairs `[ai, bi]` are **distinct**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findOrder(
        self,
        numCourses: int,
        prerequisites: List[List[int]]
    ) -> List[int]:
        parent_map = {}
        indegree_list = [0] * numCourses
        for pre in prerequisites:
            parent_map.setdefault(pre[1], []).append(pre[0])
            indegree_list[pre[0]] += 1
        
        pre_free_stack = []
        for c in range(numCourses):
            if indegree_list[c] == 0:
                # c has no pre
                pre_free_stack.append(c)
                
        ordered_courses = []
        while pre_free_stack:
            c = pre_free_stack.pop()
            ordered_courses.append(c)
            for p in parent_map.get(c, []):
                indegree_list[p] -= 1
                if indegree_list[p] == 0:
                    pre_free_stack.append(p)
        return ordered_courses if len(ordered_courses) == numCourses else []
{{< / highlight >}}
</div>
</div>
