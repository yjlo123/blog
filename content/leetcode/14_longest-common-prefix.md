---
weight: 14
title: "14 Longest Common Prefix"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string", "lc_trie"]
---

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```
**Example 2:**
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Constraints:**
- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        pre = strs[0]
        for i in range(1, len(strs)):
            while not strs[i].startswith(pre):
                pre = pre[:-1]
        return pre


'''
Sort first
'''
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        strs.sort()
        res = strs[0]
        while not strs[-1].startswith(res):
            res = res[:-1]
        return res
{{< / highlight >}}
</div>
</div>
