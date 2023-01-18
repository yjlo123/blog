---
weight: 1048
title: "1048 Longest String Chain"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_hash_table", "lc_dp", "lc_string"]
---

You are given an array of `words` where each word consists of lowercase English letters.

<code>word<sub>A</sub></code> is a **predecessor** of <code>word<sub>B</sub></code> if and only if we can insert **exactly one** letter anywhere in <code>word<sub>A</sub></code> **without changing the order of the other characters** to make it equal to <code>word<sub>B</sub></code>.

- For example, `"abc"` is a **predecessor** of `"abac"`, while `"cba"` is not a **predecessor** of `"bcad"`.

A **word chain** is a sequence of words <code>[word<sub>1</sub>, word<sub>2</sub>, ..., word<sub>k</sub>]</code> with `k >= 1`, where <code>word<sub>1</sub></code> is a **predecessor** of <code>word<sub>2</sub></code>, <code>word<sub>2</sub></code> is a **predecessor** of <code>word<sub>3</sub></code>, and so on. A single word is trivially a **word chain** with `k == 1`.

Return _the **length** of the **longest possible word chain** with words chosen from the given list of `words`_.

**Example 1:**
```
Input: words = ["a","b","ba","bca","bda","bdca"]
Output: 4
Explanation: One of the longest word chains is ["a","ba","bda","bdca"].
```
**Example 2:**
```
Input: words = ["xbc","pcxbcf","xb","cxbc","pcxbc"]
Output: 5
Explanation: All the words can be put in a word chain
["xb", "xbc", "cxbc", "pcxbc", "pcxbcf"].
```
**Example 3:**
```
Input: words = ["abcd","dbqca"]
Output: 1
Explanation: The trivial word chain ["abcd"] is one of the longest word chains.
["abcd","dbqca"] is not a valid word chain because the ordering of the letters is changed.
```

**Constraints:**
- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 16`
- `words[i]` only consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        count = defaultdict(set)
        dp = {}
        min_len = math.inf
        max_len = -math.inf
        for w in words:
            word_len = len(w)
            count[word_len].add(w)
            min_len = min(min_len, word_len)
            max_len = max(max_len, word_len)
        
        for w in count[min_len]:
            dp[w] = 1
        
        for l in range(min_len+1, max_len+1):
            for w in count[l]:
                chain_len = 1
                for i in range(len(w)):
                    pw = w[:i] + w[i+1:]
                    if pw in dp and dp[pw] + 1 > chain_len:
                        chain_len = dp[pw] + 1
                dp[w] = chain_len
        return max(dp.values())


'''
Shorter
'''
class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        dp = {}
        for w in sorted(words, key=len):
            dp[w] = max(
                dp.get(w[:i] + w[i + 1:], 0) + 1
                for i in range(len(w))
            )
        return max(dp.values())
{{< / highlight >}}
</div>
</div>
