---
weight: 3
title: "3 Longest Substring Without Repeating Characters"
date: 2020-01-01T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string", "lc_sliding_window"]
---

Given a string `s`, find the length of the **longest substring** without repeating characters.

 

**Example 1:**
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Example 4:**
```
Input: s = ""
Output: 0
```

**Constraints:**

- 0 <= s.length <= 5 * 10<sup>4</sup>
- `s` consists of English letters, digits, symbols and spaces.


<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func lengthOfLongestSubstring(s string) int {
	ans := 0 
	m := make(map[byte]int)  // "last occurred" map
	i := 0
    for j, v := range []byte(s) {
		if v, ok := m[v]; ok && v > i {
			i = v
		}
        // e.g.
        // "a": i=0, j=0, len is 0-0+1=1
        // "ab": i=0, j=1, len is 1-0+1=2
        // "aba": i=1, j=2, len is 2-1+1=2
		if j - i + 1 > ans {
			ans = j - i + 1
		}
		m[v] = j + 1
	}
	return ans
}
{{< / highlight >}}
</div>

<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        longest = 0
        d = {}
        start = 0
        for i, c in enumerate(s):
            if c in d and d[c] >= start:
                start = d[c] + 1
            d[c] = i
            longest = max(longest, i - start + 1)
        return longest
{{< / highlight >}}
</div>
</div>
