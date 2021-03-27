---
weight: 525
title: "525 Contiguous Array"
date: 2021-03-27T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```
**Note:** The length of the given binary array will not exceed 50,000.

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func findMaxLength(nums []int) int {
	m := make(map[int]int)
	m[0] = -1
	max := 0
	current := 0
	for i, v := range nums {
		if v == 0 {
			current--
		} else {
			current++
		}
		if j, ok := m[current]; ok {
			if i-j > max {
				max = i - j
			}
		} else {
			m[current] = i
		}
	}
	return max
}
{{< / highlight >}}
</div>
</div>
