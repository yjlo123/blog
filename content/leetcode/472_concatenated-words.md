---
weight: 472
title: "472 Concatenated Words"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs", "lc_dp"]
---

Given an array of strings words (**without duplicates**), return _all the **concatenated words** in the given list of words._

A **concatenated word** is defined as a string that is comprised entirely of at least two shorter words in the given array.

**Example 1:**
```
Input: words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
"dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```
**Example 2:**
```
Input: words = ["cat","dog","catdog"]
Output: ["catdog"]
```

**Constraints:**
- <code>1 <= words.length <= 10<sup>4</sup></code>
- `1 <= words[i].length <= 30`
- `words[i]` consists of only lowercase English letters.
- All the strings of words are **unique**.
- <code>1 <= sum(words[i].length) <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
        res = []
        words_dict = set(words)
        for word in words:
            words_dict.remove(word)
            if self.check(word, words_dict):
                res.append(word)
            words_dict.add(word)
        return res
    
    def check(self, word: str, d: Set[str]) -> bool:
        if word in d:
            return True
        for i in range(len(word), 0, -1):
            if word[:i] in d and self.check(word[i:], d):
                return True
        return False
{{< / highlight >}}
</div>
</div>
