---
weight: 1689
title: "1698 Number of Distinct Substrings in a String"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a string `s`, return _the number of **distinct** substrings of `s`_.

A **substring** of a string is obtained by deleting any number of characters (possibly zero) from the front of the string and any number (possibly zero) from the back of the string.

**Example 1:**
```
Input: s = "aabbaba"
Output: 21
Explanation: The set of distinct strings is
["a","b","aa","bb","ab","ba","aab","abb","bab","bba","aba","aabb",
"abba","bbab","baba","aabba","abbab","bbaba","aabbab","abbaba","aabbaba"]
```
**Example 2:**
```
Input: s = "abcdefg"
Output: 28
```

**Constraints:**
- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

**Follow up:** Can you solve this problem in `O(n)` time complexity?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def countDistinct(self, s: str) -> int:
        subs = set()
        n = len(s)
        for i in range(n):
            for j in range(i+1, n+1):
                subs.add(s[i:j])
        return len(subs)

'''
Other approaches:
1. Trie
2. Rolling hash?
'''
{{< / highlight >}}
</div>
</div>
