---
weight: 269
title: "269 Alien Dictionary"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dfs", "lc_topo_sort", "lc_string"]
---

There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary, where the strings in `words` are **sorted lexicographically** by the rules of this new language.

Return _a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules. If there is no solution, return `""`. If there are multiple solutions, return **any of them**_.

A string `s` is **lexicographically smaller** than a string `t` if at the first letter where they differ, the letter in s comes before the letter in t in the alien language. If the first `min(s.length, t.length)` letters are the same, then s is smaller if and only if `s.length < t.length`.

**Example 1:**
```
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
```
**Example 2:**
```
Input: words = ["z","x"]
Output: "zx"
```
**Example 3:**
```
Input: words = ["z","x","z"]
Output: ""
Explanation: The order is invalid, so return "".
```

**Constraints:**
- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists of only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def alienOrder(self, words: List[str]) -> str:
        reverse_adj_list = {c: [] for w in words for c in w}
        
        for w1, w2 in zip(words, words[1:]):
            for c, d in zip(w1, w2):
                if c != d:
                    reverse_adj_list[d].append(c)
                    break
            else:
                if len(w2) < len(w1):
                    # w2 is a prefix of w1
                    return ''

        def dfs(node):
            if node in seen:
                return seen[node]
            seen[node] = False  # Grey
            for n in reverse_adj_list[node]:
                if not dfs(n):
                    return False
            seen[node] = True  # Black
            res.append(node)
            return True
    
        seen = {}
        res = []
        if not all(dfs(node) for node in reverse_adj_list):
            return ''
        
        return ''.join(res)
{{< / highlight >}}
</div>
</div>
