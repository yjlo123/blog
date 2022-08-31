---
weight: 76
title: "76 Minimum Window Substring"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_sliding_window", "lc_string"]
---

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of `s` such that every character in `t` (**including duplicates**) is included in the window. If there is no such substring, return the empty string `""`._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes
'A', 'B', and 'C' from string t.
```
**Example 2:**
```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```
**Example 3:**
```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```

**Constraints:**
- `m == s.length`
- `n == t.length`
- <code>1 <= m, n <= 10<sup>5</sup></code>
- `s` and `t` consist of uppercase and lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        need = collections.Counter(t)
        missing = len(t)
        start, end = 0, 0
        i = 0
        for j, c in enumerate(s, 1):   # index j from 1
            if need[c] > 0:
                # included a char in t
                missing -= 1
            need[c] -= 1
            if missing == 0:
                # match all chars, advance left pointer
                while i < j and need[s[i]] < 0:
                    need[s[i]] += 1
                    i += 1
                # make sure the first appearing char satisfies need[char]>0
                need[s[i]] += 1
                # we missed this first char, so add missing by 1
                missing += 1
                if end == 0 or j-i < end-start:
                    start, end = i, j
                i += 1
        return s[start:end]
{{< / highlight >}}
</div>
</div>
