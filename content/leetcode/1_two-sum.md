---
weight: 1
title: "1 Two Sum"
date: 2020-09-21T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to _`target`_.

You may assume that each input would have _**exactly**_ **one solution**, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**
* 2 <= nums.length <= 10<sup>5</sup>
* -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>
* -10<sup>9</sup> <= target <= 10<sup>9</sup>
* **Only one valid answer exists.**

<div class="tabs">
  <div class="tab-btn tab-btn-active" onclick="showLang(event, 'golang')">Golang</div>
  <div class="tab-btn" onclick="showLang(event, 'python')">Python</div>
  <div class="tab-btn" onclick="showLang(event, 'java')">Java</div>
</div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func twoSum(nums []int, target int) []int {
	d := make(map[int]int)
	for idx, num := range nums {
		if v, ok := d[num]; ok {
			return []int{v, idx}
		}
		d[target-num] = idx
	}
	return nil
}
{{< / highlight >}}
</div>

<div id="python" class="lang" style="display:none">
{{< highlight python "linenos=table" >}}
def twoSum(nums: 'List[int]', target: 'int') -> 'List[int]':
	map = {}
	for i, n in enumerate(nums):
		if n in map:
			return [map[n], i]
		map[target-n] = i
{{< / highlight >}}
</div>

<div id="java" class="lang" style="display:none">
{{< highlight java "linenos=table" >}}
public int[] twoSum(int[] nums, int target) {
	Map<Integer, Integer> map = new HashMap<>();
	for (int i = 0; i < nums.length; i++) {
		int comp = target - nums[i];
		if (map.containsKey(comp)) {
			return new int[]{map.get(comp), i};
		}
		map.put(nums[i], i);
	}
	return new int[]{};
}
{{< / highlight >}}
</div>
</div>
