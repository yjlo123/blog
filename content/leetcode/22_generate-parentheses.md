---
weight: 22
title: "22 Generate Parentheses"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_back_tracking"]
---

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses._

**Example 1:**
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```
**Example 2:**
```
Input: n = 1
Output: ["()"]
```

**Constraints:**
- `1 <= n <= 8`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        def gen(left: int, right: int, cur: str) -> None:
            if left == 0 and right == 0:
                res.append(cur)
                return
            if left > 0:
                gen(left-1, right, cur + '(')
            if right > 0 and left < right:
                gen(left, right-1, cur + ')')
        gen(n, n, '')
        return res
{{< / highlight >}}
</div>
</div>
