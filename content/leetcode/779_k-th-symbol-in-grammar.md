---
weight: 779
title: "779 K-th Symbol in Grammar"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium"]
---

We build a table of `n` rows (**1-indexed**). We start by writing `0` in the <code>1<sup>st</sup></code> row. Now in every subsequent row, we look at the previous row and replace each occurrence of `0` with `01`, and each occurrence of `1` with `10`.

- For example, for `n = 3`, the <code>1<sup>st</sup></code> row is `0`, the <code>2<sup>nd</sup></code> row is `01`, and the <code>3<sup>rd</sup></code> row is `0110`.

Given two integer `n` and `k`, return the <code>k<sup>th</sup></code> (**1-indexed**) symbol in the <code>n<sup>th</sup></code> row of a table of `n` rows.


**Example 1:**
```
Input: n = 1, k = 1
Output: 0
Explanation: row 1: 0
```
**Example 2:**
```
Input: n = 2, k = 1
Output: 0
Explanation: 
row 1: 0
row 2: 01
```
**Example 3:**
```
Input: n = 2, k = 2
Output: 1
Explanation: 
row 1: 0
row 2: 01
```

**Constraints:**
- `1 <= n <= 30`
- <code>1 <= k <= 2<sup>n - 1</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def kthGrammar(self, n: int, k: int) -> int:
        if n == 1:
            return 0

        if k % 2 == 0:
            # current is right child
            if self.kthGrammar(n - 1, k // 2) == 0:
                # parent is 0, then right child is 1
                return 1
            return 0
        else:
            # current is left child
            if self.kthGrammar(n - 1, (k+1) // 2) == 0:
                # parent is 0, then left child is 0
                return 0
            return 1
{{< / highlight >}}
</div>
</div>
