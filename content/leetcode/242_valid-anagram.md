---
weight: 242
title: "242 Valid Anagram"
date: 2020-12-10T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_string"]
---

Given two strings _s_ and _t_ , write a function to determine if _t_ is an anagram of _s_.

**Example 1:**
```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**
```
Input: s = "rat", t = "car"
Output: false
```

**Constraints:**
- 1 <= `s.length`, `t.length` <= 5 * 10<sup>4</sup>
- `s` and `t` consist of lowercase English letters.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func isAnagram(s string, t string) bool {
	if len(s) != len(t) {
		return false
	}

	var count [26]int
	for _, c := range s {
		count[c-'a']++
	}
	for _, c := range t {
		count[c-'a']--
		if count[c-'a'] < 0 {
			return false
		}
	}
	return true
}
{{< / highlight >}}
</div>

<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        m = [0] * 26
        for ch in s:
            m[ord(ch) - 97] += 1
        for ch in t:
            m[ord(ch) - 97] -= 1
        for i in m:
            if i != 0:
                return False
        return True


''' Fast version '''
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return set(Counter(s).items()) == set(Counter(t).items())


''' Short version '''
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
{{< / highlight >}}
</div>
</div>
