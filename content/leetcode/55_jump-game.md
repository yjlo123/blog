---
weight: 55
title: "55 Jump Game"
date: 2021-03-18T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy"]
---

Given an array of non-negative integers `nums`, you are initially positioned at the **first index** of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**
```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what.
Its maximum jump length is 0, which makes it impossible to reach the last index.
```

**Constraints:**

- 1 <= nums.length <= 3 * 10<sup>4</sup>
- 0 <= nums[i] <= 10<sup>5</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func canJump(nums []int) bool {
	lastPos := len(nums) - 1
	for i := len(nums) - 1; i >= 0; i-- {
		if i+nums[i] >= lastPos {
			lastPos = i
		}
	}
	return lastPos == 0
}
{{< / highlight >}}
</div>
</div>
