---
weight: 660
title: "660 Remove 9"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_math"]
---

Start from integer `1`, remove any integer that contains `9` such as `9`, `19`, `29`...

Now, you will have a new integer sequence `[1, 2, 3, 4, 5, 6, 7, 8, 10, 11, ...]`.

Given an integer `n`, return the <code>n<sup>th</sup></code> (**1-indexed**) integer in the new sequence.

**Example 1:**
```
Input: n = 9
Output: 10
```
**Example 2:**
```
Input: n = 10
Output: 11
```

**Constraints:**
- <code>1 <= n <= 8 * 10<sup>8</sup></code>

> The answer is the n-th base-9 number.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def newInteger(self, n: int) -> int:
        res = ''
        while n:
            res = str(n % 9) + res
            n //= 9
        return int(res)
{{< / highlight >}}
</div>
</div>
