---
weight: 1358
title: "1358 Number of Substrings Containing All Three Characters"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_sliding_window"]
---

Given a string `s` consisting only of characters _a_, _b_ and _c_.

Return the number of substrings containing **at least** one occurrence of all these characters _a_, _b_ and _c_.

**Example 1:**
```
Input: s = "abcabc"
Output: 10
Explanation: The substrings containing at least one occurrence of the characters
a, b and c are "abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab",
"cabc" and "abc" (again). 
```
**Example 2:**
```
Input: s = "aaacb"
Output: 3
Explanation: The substrings containing at least one occurrence of the characters
a, b and c are "aaacb", "aacb" and "acb". 
```
**Example 3:**
```
Input: s = "abc"
Output: 1
```

**Constraints:**
- <code>3 <= s.length <= 5 x 10<sup>4</sup></code>
- `s` only consists of _a_, _b_ or _c_ characters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        res = i = 0
        count = {c: 0 for c in 'abc'}
        for j in range(len(s)):
            count[s[j]] += 1
            while all(count.values()):
                count[s[i]] -= 1
                i += 1
            res += i
        return res


'''
`last` will record the position of last occurrence.
If the ending index of substring is `i`,
the starting position should be on the left of min(last),
in order to have all 3 different letters.
And in this case, the starting index can be in range [0, min(last)],
min(last) + 1 in total.
'''
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        res, last = 0, [-1] * 3
        for i, c in enumerate(s):
            last[ord(c) - 97] = i
            res += 1 + min(last)
        return res
{{< / highlight >}}
</div>
</div>
