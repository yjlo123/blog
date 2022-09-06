---
weight: 696
title: "696 Count Binary Substrings"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

Given a binary string `s`, return the number of non-empty substrings that have the same number of `0`'s and `1`'s, and all the `0`'s and all the `1`'s in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

**Example 1:**
```
Input: s = "00110011"
Output: 6
Explanation: There are 6 substrings that have equal number of
consecutive 1's and 0's:
"0011", "01", "1100", "10", "0011", and "01".
Notice that some of these substrings repeat and are counted the number of
times they occur.
Also, "00110011" is not a valid substring because all the 0's (and 1's)
are not grouped together.
```
**Example 2:**
```
Input: s = "10101"
Output: 4
Explanation: There are 4 substrings: "10", "01", "10", "01" that have equal number
of consecutive 1's and 0's.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s[i]` is either `'0'` or `'1'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def countBinarySubstrings(self, s: str) -> int:
        ans = 0
        # previous group size and current group size
        # e.g. 11000 => 2,3
        prev, cur = 0, 1
        for i in range(1, len(s)):
            if s[i-1] != s[i]:
                ans += min(prev, cur)
                prev, cur = cur, 1
            else:
                cur += 1
        return ans + min(prev, cur)
{{< / highlight >}}
</div>
</div>
