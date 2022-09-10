---
weight: 231
title: "231 Power of Two"
date: 2020-10-20T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_math"]
---

Given an integer `n`, return _`true` if it is a power of two. Otherwise, return `false`_.

An integer `n` is a power of two, if there exists an integer `x` such that <code>n == 2<sup>x</sup></code>.

**Example 1:**
```
Input: n = 1
Output: true
Explanation: 2^0 = 1
```

**Example 2:**
```
Input: n = 16
Output: true
Explanation: 2^4 = 16
```

**Example 3:**
```
Input: n = 3
Output: false
```

**Example 4:**
```
Input: n = 4
Output: true
```

**Example 5:**
```
Input: n = 5
Output: false
```

**Constraints:**
- <code>-2<sup>31</sup> <= n <= 2<sup>31</sup> - 1</code>

**Follow up:** Could you solve it without loops/recursion?

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func isPowerOfTwo(n int) bool {
	i := 1
	for i < n {
		i *= 2
	}
	return i == n
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode231" target="_blank">https://runtime.siwei.dev/?src=leetcode231</a>
    </div>
</div>
</div>
