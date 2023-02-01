---
weight: 2421
title: "2421 Number of Good Paths"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_union_find"]
---

There is a tree (i.e. a connected, undirected graph with no cycles) consisting of `n` nodes numbered from `0` to `n - 1` and exactly `n - 1` edges.

You are given a 0-indexed integer array `vals` of length `n` where `vals[i]` denotes the value of the <code>i<sup>th</sup></code> node. You are also given a 2D integer array `edges` where <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> denotes that there exists an undirected edge connecting nodes <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code>.

A **good path** is a simple path that satisfies the following conditions:

The starting node and the ending node have the **same** value.
All nodes between the starting node and the ending node have values **less than or equal to** the starting node (i.e. the starting node's value should be the maximum value along the path).
Return *the number of distinct good paths*.

Note that a path and its reverse are counted as the same path. For example, `0 -> 1` is considered to be the same as `1 -> 0`. A single node is also considered as a valid path.

**Example 1:**
```
   0(1)
  /    \
1(3)   2(2)
      /    \
    3(1)   4(3)

Input: vals = [1,3,2,1,3], edges = [[0,1],[0,2],[2,3],[2,4]]
Output: 6
Explanation: There are 5 good paths consisting of a single node.
There is 1 additional good path: 1 -> 0 -> 2 -> 4.
(The reverse path 4 -> 2 -> 0 -> 1 is treated as the same as 1 -> 0 -> 2 -> 4.)
Note that 0 -> 2 -> 3 is not a good path because vals[2] > vals[0].
```
**Example 2:**
```
     0(1)
      /
    1(1)
     /
   2(2)
  /    \
3(2)   4(3)

Input: vals = [1,1,2,2,3], edges = [[0,1],[1,2],[2,3],[2,4]]
Output: 7
Explanation: There are 5 good paths consisting of a single node.
There are 2 additional good paths: 0 -> 1 and 2 -> 3.
```
**Example 3:**
```
 0(1)

Input: vals = [1], edges = []
Output: 1
Explanation: The tree consists of only one node, so there is one good path.
```

**Constraints:**
- `n == vals.length`
- <code>1 <= n <= 3 * 10<sup>4</sup></code>
- <code>0 <= vals[i] <= 10<sup>5</sup></code>
- `edges.length == n - 1`
- `edges[i].length == 2`
- <code>0 <= a<sub>i</sub>, b<sub>i</sub> < n</code>
- <code>a<sub>i</sub> != b<sub>i</sub></code>
- `edges` represents a valid tree.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfGoodPaths(self, vals: List[int], edges: List[List[int]]) -> int:
        n = len(vals)
        parent = [i for i in range(n)]
        rank = [0] * n

        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]
        
        def union(x, y):
            hx, hy = find(x), find(y)
            if hx == hy:
                return
            elif rank[hx] < rank[hy]:
                parent[hx] = hy
            elif rank[hx] > rank[hy]:
                parent[hy] = hx
            else:
                parent[hy] = hx
                rank[hx] += 1
    
        adj = defaultdict(list)
        for a, b in edges:
            adj[a].append(b)
            adj[b].append(a)
        
        val_to_nodes = defaultdict(list)
        for i in range(n):
            val_to_nodes[vals[i]].append(i)

        path_count = 0
        for val in sorted(val_to_nodes.keys()):
            # process nodes from smallest to largest value
            nodes = val_to_nodes[val]
            for node in nodes:
                if node not in adj:
                    continue
                for neighbor in adj[node]:
                    if vals[node] >= vals[neighbor]:
                        union(node, neighbor)
            group = defaultdict(int)
            for u in val_to_nodes[val]:
                hu = find(u)
                group[hu] = group[hu] + 1
            
            for size in group.values():
                path_count += size * (size + 1) // 2
        return path_count
{{< / highlight >}}
</div>
</div>
