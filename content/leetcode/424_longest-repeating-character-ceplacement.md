---
weight: 424
title: "424 Longest Repeating Character Replacement"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_sliding_window"]
---

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.

**Example 1:**
```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```
**Example 2:**
```
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        win_start = 0
        max_len = 0
        count_map = defaultdict(int)  # char count within the current window
        max_count = 0

        for win_end, c in enumerate(s):
            count_map[c] += 1
            max_count = max(max_count, count_map[c])

            if win_end - win_start + 1 - max_count > k:
                count_map[s[win_start]] -= 1
                win_start += 1
            
            max_len = max(max_len, win_end - win_start + 1)
        return max_len
{{< / highlight >}}
</div>
</div>
