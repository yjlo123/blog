---
weight: 136
title: "136 Single Number"
date: 2020-09-26T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Given a **non-empty** array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**
```
Input: [2,2,1]
Output: 1
```
**Example 2:**
```
Input: [4,1,2,1,2]
Output: 4
```
<div class="tabs">
  <div class="tab-btn tab-btn-active" onclick="showLang(event, 'golang')">Golang</div>
</div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func singleNumber(nums []int) int {
	set := make(map[int]bool)
	for _, num := range nums {
		if _, ok := set[num]; ok {
			delete(set, num)
		} else {
			set[num] = true
		}
	}
	for num, _ := range set {
		return num
	}
	return -1
}
{{< / highlight >}}
</div>
</div>