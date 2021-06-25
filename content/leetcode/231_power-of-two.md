---
weight: 231
title: "231 Power of Two"
date: 2020-10-20T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy"]
---

Given an integer n, write a function to determine if it is a power of two.

 

**Example 1:**
```
Input: n = 1
Output: true
Explanation: 20 = 1
```

**Example 2:**
```
Input: n = 16
Output: true
Explanation: 24 = 16
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

- -2<sup>31</sup> <= n <= 2<sup>31</sup> - 1


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
