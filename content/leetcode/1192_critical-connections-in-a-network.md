---
weight: 1192
title: "1192 Critical Connections in a Network"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs"]
---

There are `n` servers numbered from 0 to `n - 1` connected by undirected server-to-server `connections` forming a network where <code>connections[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> represents a connection between servers <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code>. Any server can reach other servers directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some servers unable to reach some other server.

Return _all critical connections in the network in any order_.

**Example 1:**
```
             2
           / |
         1   |
critical | \ |
         |   0
         3

Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
```
**Example 2:**
```
Input: n = 2, connections = [[0,1]]
Output: [[0,1]]
```

**Constraints:**
- <code>2 <= n <= 10<sup>5</sup></code>
- <code>n - 1 <= connections.length <= 10<sup>5</sup></code>
- <code>0 <= a<sub>i</sub>, b<sub>i</sub> <= n - 1</code>
- <code>a<sub>i</sub> != b<sub>i</sub></code>
- There are no repeated connections.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    rank = {}
    graph = defaultdict(list)
    conn_dict = {}
    
    def criticalConnections(
        self,
        n: int,
        connections: List[List[int]]
    ) -> List[List[int]]:
        self.formGraph(n, connections)
        self.dfs(0, 0)
        
        return [[u, v] for u, v in self.conn_dict]
            
    def dfs(self, node: int, discovery_rank: int) -> int:
        # node is already visited
        if self.rank[node]:
            return self.rank[node]
        
        # Update rank
        self.rank[node] = discovery_rank
        
        # This is the max we have seen till now.
        # So we start with this instead of INT_MAX or something.
        min_rank = discovery_rank + 1
        for neighbor in self.graph[node]:
            # Skip the parent.
            if self.rank[neighbor] and self.rank[neighbor] == discovery_rank - 1:
                continue
            recursive_rank = self.dfs(neighbor, discovery_rank + 1)
            # Step 1, check if this edge needs to be discarded.
            if recursive_rank <= discovery_rank:
                del self.conn_dict[(min(node, neighbor), max(node, neighbor))]
            # Step 2, update the minRank if needed.
            min_rank = min(min_rank, recursive_rank)

        return min_rank
    
    def formGraph(self, n: int, connections: List[List[int]]):
        # Reinitialize for each test case
        self.rank = {}
        self.graph = defaultdict(list)
        self.conn_dict = {}
        
        # Default rank for unvisited nodes is "null"
        for i in range(n):
            self.rank[i] = None
        
        for edge in connections:
            # Bidirectional edges.
            u, v = edge[0], edge[1]
            self.graph[u].append(v)
            self.graph[v].append(u)
            self.conn_dict[(min(u, v), max(u, v))] = 1
{{< / highlight >}}
</div>
</div>
