---
weight: 131
title: "131 Palindrome Partitioning"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_dp"]
---

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```
**Example 2:**
```
Input: s = "a"
Output: [["a"]]
```

**Constraints:**
- `1 <= s.length <= 16`
- `s` contains only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        if not s: return [[]]
        ans = []
        for i in range(1, len(s) + 1):
            if s[:i] == s[:i][::-1]:  # prefix is a palindrome
                for suf in self.partition(s[i:]):
                    ans.append([s[:i]] + suf)
        return ans
{{< / highlight >}}
</div>
</div>
