---
weight: 316
title: "316 Remove Duplicate Letters"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack"]
---

Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.

**Example 1:**
```
Input: s = "bcabc"
Output: "abc"
```
**Example 2:**
```
Input: s = "cbacdcbc"
Output: "acdb"
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        stack = []
        seen = set()
        last_occur = {c: i for i, c in enumerate(s)}
        
        for i, c in enumerate(s):
            if c not in seen:
                while stack and c < stack[-1] and i < last_occur[stack[-1]]:
                    seen.remove(stack.pop())
                seen.add(c)
                stack.append(c)
        return ''.join(stack)
{{< / highlight >}}
</div>
</div>
