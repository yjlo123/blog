---
weight: 525
title: "525 Contiguous Array"
date: 2021-03-27T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

Given a binary array `nums`, return _the maximum length of a contiguous subarray with an equal number of `0` and `1`_.

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

**Constraints:**
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- `nums[i]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        max_len = 0
        h = {}
        count = 0
        for i, n in enumerate(nums):
            count += 1 if n == 1 else -1
            
            if count == 0:
                max_len = i + 1
            if count in h:
                max_len = max(max_len, i - h[count])
            else:
                h[count] = i
        return max_len
{{< / highlight >}}
</div>

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
