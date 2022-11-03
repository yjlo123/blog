---
weight: 60
title: "60 Permutation Sequence"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_math"]
---

The set `[1, 2, 3, ..., n]` contains a total of `n!` unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for `n = 3`:  
`"123"`  
`"132"`  
`"213"`  
`"231"`  
`"312"`  
`"321"`  
Given `n` and `k`, return the <code>k<sup>th</sup></code> permutation sequence.

**Example 1:**
```
Input: n = 3, k = 3
Output: "213"
```
**Example 2:**
```
Input: n = 4, k = 9
Output: "2314"
```
**Example 3:**
```
Input: n = 3, k = 1
Output: "123"
```

**Constraints:**
- `1 <= n <= 9`
- `1 <= k <= n!`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def getPermutation(self, n: int, k: int) -> str:
        elements = list(range(1, n+1))
        f = math.factorial(n)
        k -= 1
        res = ''
        while len(elements) > 0:
            f //= len(elements)
            i, k = k // f, k % f
            res += str(elements.pop(i))
        return res
{{< / highlight >}}
</div>
</div>
