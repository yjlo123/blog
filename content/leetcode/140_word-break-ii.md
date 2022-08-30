---
weight: 140
title: "140 Word Break II"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_back_tracking"]
---

Given a string `s` and a dictionary of strings `wordDict`, add spaces in `s` to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in **any order**.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**
```
Input: s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
Output: ["cats and dog","cat sand dog"]
```
**Example 2:**
```
Input: s = "pineapplepenapple", wordDict = ["apple","pen","applepen","pine","pineapple"]
Output: ["pine apple pen apple","pineapple pen apple","pine applepen apple"]
Explanation: Note that you are allowed to reuse a dictionary word.
```
**Example 3:**
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: []
```

**Constraints:**
- `1 <= s.length <= 20`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 10`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of wordDict are **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        res = []
        self.back_tracking(s, wordDict, res, [])
        return res
        
    def back_tracking(
        self, s: str,
        d: list[str],
        res: List[str],
        track: List[str]
    ) -> None:
        if not s:
            res.append(' '.join(track))
        for w in d:
            if s.startswith(w):
                self.back_tracking(s[len(w):], d, res, track+[w])
{{< / highlight >}}
</div>
</div>
