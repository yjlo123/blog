---
weight: 17
title: "17 Letter Combinations of a Phone Number"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```
   1       2(abc)  3(def)
   4(ghi)  5(jkl)  6(mno)
   7(pqrs) 8(tuv)  9(wxyz)
   *+      0_      ^#
```

**Example 1:**
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```
**Example 2:**
```
Input: digits = ""
Output: []
```
**Example 3:**
```
Input: digits = "2"
Output: ["a","b","c"]
```

**Constraints:**
- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        M = [0, 1, 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
        res = ['']
        for c in digits:
            res = [p+n for p in res for n in M[int(c)]]
        return res
{{< / highlight >}}
</div>
</div>
