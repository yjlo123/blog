---
weight: 247
title: "247 H-Index"
date: 2021-03-17T00:00:00+08:00
draft: false
tags: ["leetcode0", "lc_medium", "lc_bucket_sort"]
---

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their i<sup>th</sup> paper, return compute the researcher's `h`**-index**.

According to the `definition of h-index on Wikipedia`: A scientist has an index `h` if `h` of their `n` papers have at least h citations each, and the other `n − h` papers have no more than `h` citations each.

If there are several possible values for `h`, the maximum one is taken as the `h`**-index**.

**Example 1:**
```
Input: citations = [3,0,6,1,5]
Output: 3
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total
and each of them had received 3, 0, 6, 1, 5 citations respectively.
Since the researcher has 3 papers with at least 3 citations each and
the remaining two with no more than 3 citations each, their h-index is 3.
```
**Example 2:**
```
Input: citations = [1,3,1]
Output: 1
```

**Constraints:**

- n == citations.length
- 1 <= n <= 5000
- 0 <= citations[i] <= 1000

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func hIndex(citations []int) int {
	buckets := make([]int, len(citations)+1)
	length := len(citations)
	for _, c := range citations {
		if c >= length {
			buckets[length]++
		} else {
			buckets[c]++
		}
	}

	count := 0
	for i := length; i > 0; i-- {
		count += buckets[i]
		if count >= i {
			return i
		}
	}
	return 0
}
{{< / highlight >}}
</div>
</div>
