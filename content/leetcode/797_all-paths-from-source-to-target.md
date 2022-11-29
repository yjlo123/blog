---
weight: 797
title: "797 All Paths From Source to Target"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dfs", "lc_back_tracking"]
---

Given a directed acyclic graph (**DAG**) of n nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in any order.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node i to node `graph[i][j]`).

**Example 1:**
```
(0)-->(1)
 |     |
 v     v
(2)-->(3)

Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```
**Example 2:**
```
 --------.
/   (0)->(1)
|   / \  / \
|  v   v    v
->(4)<(3)<-(2)

Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```

**Constraints:**
- `n == graph.length`
- `2 <= n <= 15`
- `0 <= graph[i][j] < n`
- `graph[i][j] != i` (i.e., there will be no self-loops).
- All the elements of `graph[i]` are **unique**.
- The input graph is **guaranteed** to be a **DAG**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        path = []
        n = len(graph)
        res = []
        def dfs(current: int) -> None:
            if current == n-1:
                res.append(path + [current])
                return
            path.append(current)
            for nxt in graph[current]:
                dfs(nxt)
            path.pop()
        dfs(0)
        return res
{{< / highlight >}}
</div>
</div>
