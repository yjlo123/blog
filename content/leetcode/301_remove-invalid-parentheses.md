---
weight: 301
title: "301 Remove Invalid Parentheses"
date: 2022-10-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_bfs", "lc_back_tracking"]
---

Given a string `s` that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return _all the possible results_. You may return the answer in **any order**.


**Example 1:**
```
Input: s = "()())()"
Output: ["(())()","()()()"]
```
**Example 2:**
```
Input: s = "(a)())()"
Output: ["(a())()","(a)()()"]
```
**Example 3:**
```
Input: s = ")("
Output: [""]
```

**Constraints:**
- `1 <= s.length <= 25`
- `s` consists of lowercase English letters and parentheses `'('` and `')'`.
- There will be at most `20` parentheses in `s`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        def is_valid(string: str) -> bool:
            count = 0
            for c in string:
                if c == '(':
                    count += 1
                elif c == ')':
                    count -= 1
                    if count < 0:
                        return False
            return count == 0
        
        level = {s}
        while True:
            valid = list(filter(is_valid, level))
            if valid:
                return valid
            level = {
                w[:i] + w[i+1:]
                for w in level
                for i in range(len(w))
                if w[i] in {'(', ')'}
            }
        return ['']
{{< / highlight >}}
</div>
</div>
