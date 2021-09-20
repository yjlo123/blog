---
weight: 567
title: "567 Permutation in String"
date: 2021-09-19T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_sliding_window"]
---

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```
**Example 2:**
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```

**Constraints:**
- 1 <= s1.length, s2.length <= 10<sup>4</sup>
- `s1` and `s2` consist of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        l1 = [0]*26
        l2 = [0]*26
        for x in s1:
            l1[ord(x) - ord('a')] += 1
        
        for i in range(len(s2)):
            l2[ord(s2[i]) - ord('a')] += 1
            if i >= len(s1):
                l2[ord(s2[i-len(s1)]) - ord('a')] -= 1
            if l1 == l2:
                return True
        return False
{{< / highlight >}}
</div>
</div>
