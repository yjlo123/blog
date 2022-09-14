---
weight: 57
title: "57 Insert Interval"
date: 2021-03-19T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array"]
---

You are given an array of non-overlapping `intervals` intervals where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represent the start and the end of the <code>i<sup>th</sup></code> interval and `intervals` is sorted in ascending order by <code>start<sub>i</sub></code>. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by <code>start<sub>i</sub></code> and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return _`intervals` after the insertion_.

**Example 1:**
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```
**Example 2:**
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```
**Example 3:**
```
Input: intervals = [], newInterval = [5,7]
Output: [[5,7]]
```
**Example 4:**
```
Input: intervals = [[1,5]], newInterval = [2,3]
Output: [[1,5]]
```
**Example 5:**
```
Input: intervals = [[1,5]], newInterval = [2,7]
Output: [[1,7]]
```

**Constraints:**
- <code>0 <= intervals.length <= 10<sup>4</sup></code>
- `intervals[i].length == 2`
- <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>5</sup></code>
- `intervals` is sorted by <code>start<sub>i</sub></code> in **ascending** order.
- `newInterval.length == 2`
- <code>0 <= start <= end <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def insert(
		self,
		intervals: List[List[int]],
		newInterval: List[int]
	) -> List[List[int]]:
        s, e = newInterval
        left, right = [], []
        for i in intervals:
            if i[1] < s:
                left.append(i),
            elif i[0] > e:
                right.append(i),
            else:
                s = min(s, i[0])
                e = max(e, i[1])
        return left + [[s, e]] + right
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func insert(intervals [][]int, newInterval []int) [][]int {
	result := make([][]int, 0)
	i := 0
	for i < len(intervals) && intervals[i][1] < newInterval[0] {
		result = append(result, intervals[i])
		i++
	}

	for i < len(intervals) && intervals[i][0] <= newInterval[1] {
		newInterval = []int{
			Min(newInterval[0], intervals[i][0]),
			Max(newInterval[1], intervals[i][1]),
		}
		i++
	}
	result = append(result, newInterval)
	for i < len(intervals) {
		result = append(result, intervals[i])
		i++
	}
	return result
}
{{< / highlight >}}
</div>
</div>
