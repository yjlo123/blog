---
weight: 247
title: "247 Strobogrammatic Number II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

Given an integer `n`, return all the **strobogrammatic numbers** that are of length `n`. You may return the answer in **any order**.

A **strobogrammatic number** is a number that looks the same when rotated `180` degrees (looked at upside down).

**Example 1:**
```
Input: n = 2
Output: ["11","69","88","96"]
```
**Example 2:**
```
Input: n = 1
Output: ["0","1","8"]
```

**Constraints:**
- `1 <= n <= 14`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findStrobogrammatic(self, n: int) -> List[str]:
        middle = ['0', '1', '8']
        pairs = ['00', '11', '88', '69', '96']
        
        res = []
        def wrap(m, s):
            if m == 0:
                res.append(s)
                return
            for pair in pairs:
                if m == 1 and pair[0] == '0':
                    continue
                wrap(m - 1, pair[0] + s + pair[1])

        if n % 2 == 0:
            wrap(n // 2, '')
        else:
            for m in middle:
                wrap(n // 2, m)
        return res
                
{{< / highlight >}}
</div>
</div>
