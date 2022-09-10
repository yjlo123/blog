---
weight: 767
title: "767 Reorganize String"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a string `s`, rearrange the characters of `s` so that any two adjacent characters are not the same.

Return _any possible rearrangement of `s` or return `""` if not possible_.

**Example 1:**
```
Input: s = "aab"
Output: "aba"
```
**Example 2:**
```
Input: s = "aaab"
Output: ""
```

**Constraints:**
- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def reorganizeString(self, s: str) -> str:
        counts = [0] * 26
        most_common_char = 0
        most_common_count = 0
        for c in s:
            idx = ord(c) - ord('a')
            counts[idx] += 1
            if counts[idx] > most_common_count:
                most_common_char = c
                most_common_count = counts[idx]
        sub_chars = [most_common_char] * most_common_count
        
        rest = ''
        for i in range(26):
            char = chr(i + ord('a'))
            if char == most_common_char:
                continue
            rest += (char * counts[i])
            
        if len(rest) < most_common_count - 1:
            return ''
        
        i = 0
        for c in rest:
            sub_chars[i] += c
            i = (i + 1) % most_common_count
        return ''.join(sub_chars)
{{< / highlight >}}
</div>
</div>
