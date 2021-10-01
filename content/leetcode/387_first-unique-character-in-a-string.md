---
weight: 387
title: "387 First Unique Character in a String"
date: 2020-12-20T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_hash_table", "lc_string"]
---

Given a string `s`, _find the first non-repeating character in it and return its index_. If it does not exist, return `-1`.

**Example 1:**
```
Input: s = "leetcode"
Output: 0
```

**Example 2:**
```
Input: s = "loveleetcode"
Output: 2
```

**Example 3:**
```
Input: s = "aabb"
Output: -1
```

**Constraints:**
- 1 <= `s.length` <= 10<sup>5</sup>
- `s` consists of only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func firstUniqChar(s string) int {
	m := make(map[rune]int)
	for _, c := range s {
		_, has := m[c]
		if has {
			m[c]++
		} else {
			m[c] = 1
		}
	}

	for i, c := range s {
		if m[c] == 1 {
			return i
		}
	}
	return -1
}
{{< / highlight >}}
</div>

<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def firstUniqChar(self, s: str) -> int:
        count = collections.Counter(s)

        for idx, ch in enumerate(s):
            if count[ch] == 1:
                return idx     
        return -1


''' Fast version '''
class Solution:
    def firstUniqChar(self, s: str) -> int:
        letters='abcdefghijklmnopqrstuvwxyz'
        index=[s.index(l) for l in letters if s.count(l) == 1]
        return min(index) if len(index) > 0 else -1
{{< / highlight >}}
</div>
</div>
