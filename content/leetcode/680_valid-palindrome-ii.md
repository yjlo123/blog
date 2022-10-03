---
weight: 680
title: "680 Valid Palindrome II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string", "lc_two_pointers"]
---

Given a string `s`, return _`true` if the `s` can be palindrome after deleting **at most one** character from it_.

**Example 1:**
```
Input: s = "aba"
Output: true
```
**Example 2:**
```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```
**Example 3:**
```
Input: s = "abc"
Output: false
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def validPalindrome(self, s: str) -> bool:
        if s == s[::-1]:
            return True

        def rec(l, r) -> bool:
            if l >= r:
                return True
            if s[l] == s[r]:
                return rec(l + 1, r - 1)
            temp1 = s[l+1:r+1]
            temp2 = s[l:r]
            return (
                temp1 == temp1[::-1] or
                temp2 == temp2[::-1]
            )
        return rec(0, len(s) - 1)
{{< / highlight >}}
</div>
</div>
