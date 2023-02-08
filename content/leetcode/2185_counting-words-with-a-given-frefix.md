---
weight: 2185
title: "2185 Counting Words With a Given Prefix"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

You are given an array of strings `words` and a string `pref`.

Return *the number of strings in `words` that contain `pref` as a **prefix***.

A **prefix** of a string `s` is any leading contiguous substring of `s`.

**Example 1:**
```
Input: words = ["pay","attention","practice","attend"], pref = "at"
Output: 2
Explanation: The 2 strings that contain "at" as a prefix are: "attention" and "attend".
```
**Example 2:**
```
Input: words = ["leetcode","win","loops","success"], pref = "code"
Output: 0
Explanation: There are no strings that contain "code" as a prefix.
```

**Constraints:**
- `1 <= words.length <= 100`
- `1 <= words[i].length, pref.length <= 100`
- `words[i]` and `pref` consist of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def prefixCount(self, words: List[str], pref: str) -> int:
        return sum(w.startswith(pref) for w in words)
{{< / highlight >}}
</div>
</div>

**Follow-up:**  
**Q**: What if the words are sorted lexicographically?  
**A**: We can use binary search twice to locate the lower and upper bounds of the words that have the same prefix. Therefore, the time cost is `O(klogn)`. e.g.,
Assume `perf = "abcd"`, we can search `"abcd"` and `"abce"` respectively.