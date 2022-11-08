---
weight: 332
title: "332 Reconstruct Itinerary"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs", "lc_back_tracking"]
---

You are given a list of airline `tickets` where <code>tickets[i] = [from<sub>i</sub>, to<sub>i</sub>]</code> represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

- For example, the itinerary `["JFK", "LGA"]` has a smaller lexical order than `["JFK", "LGB"]`.

You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.

**Example 1:**
```
MUC --> LHR --> SFO
 ^               |
 |               v
JFK             SJC

Input: tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
Output: ["JFK","MUC","LHR","SFO","SJC"]
```
**Example 2:**
```
SFO <-.
 ^   \ \
 |     \ \
 |  --> v |
JFK <-- ATL

Input: tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]
but it is larger in lexical order.
```

**Constraints:**
- `1 <= tickets.length <= 300`
- `tickets[i].length == 2`
- <code>from<sub>i</sub>.length == 3</code>
- <code>to<sub>i</sub>.length == 3</code>
- <code>from<sub>i</sub></code> and <code>to<sub>i</sub></code> consist of uppercase English letters.
- <code>from<sub>i</sub> != to<sub>i</sub></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import defaultdict

class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        self.graph = defaultdict(list)

        for src, des in tickets:
            self.graph[src].append(des)

        self.visit_map = {}

        # sort the itinerary based on the lexical order
        for origin, destinations in self.graph.items():
            # Note that we could have multiple identical flights,
            # i.e. same origin and destination.
            destinations.sort()
            self.visit_map[origin] = [False] * len(destinations)

        self.n = len(tickets)
        self.result = []
        route = ['JFK']
        self.backtracking('JFK', route)

        return self.result

    def backtracking(self, src, route):
        if len(route) == self.n + 1:
            self.result = route
            # since the itineraries are sorted, we can stop
            # once the first one is found
            return True

        for i, next_des in enumerate(self.graph[src]):
            if not self.visit_map[src][i]:
                # mark the visit before the next recursion
                self.visit_map[src][i] = True
                ret = self.backtracking(next_des, route + [next_des])
                self.visit_map[src][i] = False
                if ret:
                    return True
        return False
{{< / highlight >}}
</div>
</div>
