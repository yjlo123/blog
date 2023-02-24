---
weight: 55
title: "55 Jump Game"
date: 2021-03-18T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy", "lc_dp"]
---

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return _`true` if you can reach the last index, or `false` otherwise._

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

- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>0 <= nums[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
"""
Greedy
"""
class Solution:

    # Forward version:
    def canJump(self, nums: List[int]) -> bool:
        last = len(nums) - 1
        for i in range(len(nums) - 1, -1, -1):
            if i + nums[i] >= last:
                last = i
        return last == 0

    # Backward version:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        farthest = 0
        for i in range(n-1):
            farthest = max(farthest, i + nums[i])
            if farthest <= i:
                # stcuk at i
                return False
        return farthest >= n-1

"""
DP
"""
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        dp = [False] * n
        dp[-1] = True
        for i in range(n-2, -1, -1):
            furthest = min(i + nums[i], n-1)
            if any(dp[i+1:furthest+1]):
                dp[i] = True
        return dp[0]
{{< / highlight >}}
</div>

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
