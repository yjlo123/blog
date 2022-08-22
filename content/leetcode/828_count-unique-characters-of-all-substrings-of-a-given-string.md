---
weight: 828
title: "828 Count Unique Characters of All Substrings of a Given String"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_string"]
---

Let's define a function `countUniqueChars(s)` that returns the number of unique characters on `s`.

- For example, calling `countUniqueChars(s)` if `s = "LEETCODE"` then `"L"`, `"T"`, `"C"`, `"O"`, `"D"` are the unique characters since they appear only once in `s`, therefore `countUniqueChars(s) = 5`.
Given a string `s`, return the sum of `countUniqueChars(t)` where `t` is a substring of `s`. The test cases are generated such that the answer fits in a 32-bit integer.

Notice that some substrings can be repeated so in this case you have to count the repeated ones too.

**Example 1:**
```
Input: s = "ABC"
Output: 10
Explanation: All possible substrings are: "A","B","C","AB","BC" and "ABC".
Every substring is composed with only unique letters.
Sum of lengths of all substring is 1 + 1 + 1 + 2 + 2 + 3 = 10
```
**Example 2:**
```
Input: s = "ABA"
Output: 8
Explanation: The same as example 1, except countUniqueChars("ABA") = 1.
```
**Example 3:**
```
Input: s = "LEETCODE"
Output: 92
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of uppercase English letters only.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def uniqueLetterString(self, s: str) -> int:
        '''
        https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/discuss/128952/JavaC++Python-One-pass-O(N)
        '''
        index = {c: [-1, -1] for c in "ABCDEFGHIJKLMNOPQRSTUVWXYZ"}
        res = 0
        for i, c in enumerate(s):
            k, j = index[c]
            res += (i - j) * (j - k)
            index[c] = [j, i]
        for c in index:
            k, j = index[c]
            res += (len(s) - j) * (j - k)
        return res
{{< / highlight >}}
</div>
</div>
