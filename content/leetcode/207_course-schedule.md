---
weight: 207
title: "207 Course Schedule"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs"]
---

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```
**Example 2:**
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0
you should also have finished course 1. So it is impossible.
```

**Constraints:**
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
- All the pairs `prerequisites[i]` are **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def canFinish(
        self,
        numCourses: int,
        prerequisites: List[List[int]]
    ) -> bool:
        child_map = {}
        for p in prerequisites:
            child_map.setdefault(p[0], []).append(p[1])
        # 0: not_visited, 1: being_visited, 2: visited
        visited = [0] * numCourses

        for c in range(numCourses):
            if not self.is_valid(c, visited, child_map):
                return False
        return True
        
    def is_valid(
        self,
        c: int,
        visited: List[int],
        child_map: Dict[int, List[int]]
    ) -> bool:
        """ DFS """
        if visited[c] == 2 or c not in child_map:
            return True
        if visited[c] == 1:
            return False

        visited[c] = 1
        for child in child_map[c]:
            if not self.is_valid(child, visited, child_map):
                return False
        visited[c] = 2
        return True
{{< / highlight >}}
</div>
</div>
