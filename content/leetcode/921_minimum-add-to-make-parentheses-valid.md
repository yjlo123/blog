---
weight: 921
title: "921 Minimum Add to Make Parentheses Valid"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack", "lc_greedy"]
---

A parentheses string is valid if and only if:
- It is the empty string,
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

You are given a parentheses string `s`. In one move, you can insert a parenthesis at any position of the string.

- For example, if `s = "()))"`, you can insert an opening parenthesis to be `"(()))"` or a closing parenthesis to be `"())))"`.
Return *the minimum number of moves required to make `s` valid*.

**Example 1:**
```
Input: s = "())"
Output: 1
```
**Example 2:**
```
Input: s = "((("
Output: 3
```

**Constraints:**
- `1 <= s.length <= 1000`
- `s[i]` is either `'('` or `')'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minAddToMakeValid(self, s: str) -> int:
        count = 0
        stack = 0
        for c in s:
            if c == '(':
                stack += 1
            elif stack:
                stack -= 1
            else:
                count += 1
        return count + stack
{{< / highlight >}}
</div>
</div>
