---
weight: 1245
title: "1245 Tree Diameter"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_dfs", "lc_bfs"]
---

The **diameter** of a tree is **the number of edges** in the longest path in that tree.

There is an undirected tree of `n` nodes labeled from `0` to `n - 1`. You are given a 2D array `edges` where `edges.length == n - 1` and <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that there is an undirected edge between nodes <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code> in the tree.

Return _the **diameter** of the tree_.

**Example 1:**
```
  0
 / \
2   1

Input: edges = [[0,1],[0,2]]
Output: 2
Explanation: The longest path of the tree is the path 1 - 0 - 2.
```
**Example 2:**
```
   1
 / | \
0  2  4
   |  |
   3  5

Input: edges = [[0,1],[1,2],[2,3],[1,4],[4,5]]
Output: 4
Explanation: The longest path of the tree is the path 3 - 2 - 1 - 4 - 5.
```

**Constraints:**
- `n == edges.length + 1`
- <code>1 <= n <= 10<sup>4</sup></code>
- <code>0 <= a<sub>i</sub>, b<sub>i</sub> < n</code>
- <code>a<sub>i</sub> != b<sub>i</sub></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
'''
DFS
'''
from collections import defaultdict
class Solution:
    def treeDiameter(self, edges: List[List[int]]) -> int:
        graph = defaultdict(list)
        for s, d in edges:
            graph[s].append(d)
            graph[d].append(s)
        
        def dfs(node: int) -> int:
            top_dis1, top_dis2 = 0, 0
            visited.add(node)
            dis = 0

            for c in graph[node]:
                if c not in visited:
                    dis = 1 + dfs(c)
                if dis > top_dis1:
                    top_dis1, top_dis2 = dis, top_dis1
                elif dis > top_dis2:
                    top_dis2 = dis

            self.diameter = max(self.diameter, top_dis1 + top_dis2)
            return top_dis1

        self.diameter = 0
        visited = set()
        dfs(0)
        return self.diameter


'''
2-time BFS
'''
class Solution:
    def treeDiameter(self, edges: List[List[int]]) -> int:
        graph = defaultdict(list)
        for s, d in edges:
            graph[s].append(d)
            graph[d].append(s)
    
        def bfs(node: int) -> Tuple[int, int]:
            visited = set([node])
            last_node = -1
            dis = -1
            q = [node]
            while q:
                temp_q = []
                for n in q:
                    for child in graph[n]:
                        if child not in visited:
                            visited.add(child)
                            temp_q.append(child)
                            last_node = child
                dis += 1
                q = temp_q
            return last_node, dis
        
        far_node_1, dis_1 = bfs(0)
        far_node_2, dis_2 = bfs(far_node_1)

        return dis_2
{{< / highlight >}}
</div>
</div>
