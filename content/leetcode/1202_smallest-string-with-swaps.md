---
weight: 1202
title: "1202 Smallest String With Swaps"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_union_find"]
---

You are given a string `s`, and an array of pairs of indices in the string `pairs` where `pairs[i] = [a, b]` indicates 2 indices(0-indexed) of the string.

You can swap the characters at any pair of indices in the given `pairs` **any number of times**.

Return the lexicographically smallest string that `s` can be changed to after using the swaps.

**Example 1:**
```
Input: s = "dcab", pairs = [[0,3],[1,2]]
Output: "bacd"
Explaination: 
Swap s[0] and s[3], s = "bcad"
Swap s[1] and s[2], s = "bacd"
```
**Example 2:**
```
Input: s = "dcab", pairs = [[0,3],[1,2],[0,2]]
Output: "abcd"
Explaination: 
Swap s[0] and s[3], s = "bcad"
Swap s[0] and s[2], s = "acbd"
Swap s[1] and s[2], s = "abcd"
```
**Example 3:**
```
Input: s = "cba", pairs = [[0,1],[1,2]]
Output: "abc"
Explaination: 
Swap s[0] and s[1], s = "bca"
Swap s[1] and s[2], s = "bac"
Swap s[0] and s[1], s = "abc"
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- <code>0 <= pairs.length <= 10<sup>5</sup></code>
- `0 <= pairs[i][0], pairs[i][1] < s.length`
- `s` only contains lower case English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def smallestStringWithSwaps(self, s: str, pairs: List[List[int]]) -> str:
        class UF:
            def __init__(self, n):
                self.p = list(range(n))

            def union(self, x, y):
                self.p[self.find(x)] = self.find(y)

            def find(self, x):
                if x != self.p[x]:
                    self.p[x] = self.find(self.p[x])
                return self.p[x]

        n = len(s)
        uf = UF(n)
        res = []
        group = defaultdict(list)

        for x, y in pairs:
            uf.union(x, y)

        for i in range(n): 
            group[uf.find(i)].append(s[i])

        for gid in group.keys(): 
            group[gid].sort(reverse=True)

        for i in range(n): 
            res.append(group[uf.find(i)].pop())

        return ''.join(res)
{{< / highlight >}}
</div>
</div>
