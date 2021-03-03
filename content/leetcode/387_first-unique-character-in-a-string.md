---
weight: 387
title: "387 First Unique Character in a String"
date: 2020-12-20T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy"]
---

Given a string, find the first non-repeating character in it and return its index. If it doesn't exist, return -1.

**Examples:**
```
s = "leetcode"
return 0.

s = "loveleetcode"
return 2.
```

**Note:** You may assume the string contains only lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func firstUniqChar(s string) int {
	m := make(map[rune]int)
	for i, c := range s {
		_, has := m[c]
		if has {
			m[c] = -1
		} else {
			m[c] = i
		}
	}
	const maxInt = int(^uint(0) >> 1)
	min := maxInt
	for _, i := range m {
		if i > -1 && i < min {
			min = i
		}
	}
	if min == maxInt {
		return -1
	}
	return min
}
{{< / highlight >}}
</div>
</div>
