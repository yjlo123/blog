---
weight: 1790
title: "1790 Check if One String Swap Can Make Strings Equal
"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

You are given two strings `s1` and `s2` of equal length. A **string swap** is an operation where you choose two indices in a string (not necessarily different) and swap the characters at these indices.

Return _`true` if it is possible to make both strings equal by performing **at most one string swap** on exactly one of the strings_. Otherwise, return _`false`_.

**Example 1:**
```
Input: s1 = "bank", s2 = "kanb"
Output: true
Explanation: For example, swap the first character with the last character
of s2 to make "bank".
```
**Example 2:**
```
Input: s1 = "attack", s2 = "defend"
Output: false
Explanation: It is impossible to make them equal with one string swap.
```
**Example 3:**
```
Input: s1 = "kelb", s2 = "kelb"
Output: true
Explanation: The two strings are already equal,
so no string swap operation is required.
```

**Constraints:**
- `1 <= s1.length, s2.length <= 100`
- `s1.length == s2.length`
- `s1` and `s2` consist of only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def areAlmostEqual(self, s1: str, s2: str) -> bool:
        if len(s1) != len(s2):
            return False
        first_diff_idx, second_diff_idx = -1, -1
        for i in range(len(s1)):
            c1, c2 = s1[i], s2[i]
            if c1 != c2:
                if first_diff_idx == -1:
                    first_diff_idx = i
                elif second_diff_idx == -1:
                    second_diff_idx = i
                else:
                    return False
        return (
            s1[first_diff_idx] == s2[second_diff_idx]
            and s1[second_diff_idx] == s2[first_diff_idx]
        )
{{< / highlight >}}
</div>
</div>
