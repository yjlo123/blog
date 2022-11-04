---
weight: 159
title: "159 Longest Substring with At Most Two Distinct Characters"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_two_pointers"]
---

Given a string `s`, return _the length of the longest 
substring (A substring is a contiguous non-empty sequence of characters within a string.) that contains at most **two distinct characters**_.

**Example 1:**
```
Input: s = "eceba"
Output: 3
Explanation: The substring is "ece" which its length is 3.
```
**Example 2:**
```
Input: s = "ccaabbb"
Output: 5
Explanation: The substring is "aabbb" which its length is 5.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        left = right = -1
        d = defaultdict(int)
        res = 0
        while right < len(s)-1:
            right += 1
            d[s[right]] += 1
            while len(d) > 2:
                left += 1
                d[s[left]] -= 1
                if d[s[left]] == 0:
                    del d[s[left]]
            res = max(res, right-left)
        return res
{{< / highlight >}}
</div>
</div>
