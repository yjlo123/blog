---
weight: 1055
title: "1055 Shortest Way to Form String"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_greedy", "lc_two_pointers"]
---

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

Given two strings `source` and `target`, return *the minimum number of subsequences of `source` such that their concatenation equals `target`*. If the task is impossible, return `-1`.


**Example 1:**
```
Input: source = "abc", target = "abcbc"
Output: 2
Explanation: The target "abcbc" can be formed by "abc" and "bc",
which are subsequences of source "abc".
```
**Example 2:**
```
Input: source = "abc", target = "acdbc"
Output: -1
Explanation: The target string cannot be constructed from the subsequences of
source string due to the character "d" in target string.
```
**Example 3:**
```
Input: source = "xyz", target = "xzyxz"
Output: 3
Explanation: The target string can be constructed as follows "xz" + "y" + "xz".
```

**Constraints:**
- `1 <= source.length, target.length <= 1000`
- `source` and `target` consist of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def shortestWay(self, source: str, target: str) -> int:
        char_to_indices = defaultdict(list)
        for i, c in enumerate(source):
            char_to_indices[c].append(i)

        i = 0  # source_iterator
        count = 1

        for c in target:
            if c not in char_to_indices:
                return -1

            # Binary Search to find the index of the character in source
            # next to the current i
            index = bisect.bisect_left(char_to_indices[c], i)

            # If we have reached the end of the list, we need to iterate
            # through source again, hence first index of character in source.
            if index == len(char_to_indices[c]):
                count += 1
                i = char_to_indices[c][0] + 1
            else:
                i = char_to_indices[c][index] + 1
        return count
{{< / highlight >}}
</div>
</div>
