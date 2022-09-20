---
weight: 274
title: "274 H-Index"
date: 2021-03-17T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_bucket_sort"]
---

Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their <code>i<sup>th</sup></code> paper, return compute the researcher's `h`**-index**.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): A scientist has an index `h` if `h` of their `n` papers have at least h citations each, and the other `n − h` papers have no more than `h` citations each.

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

- `n == citations.length`
- `1 <= n <= 5000`
- `0 <= citations[i] <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        n = len(citations)
        counts = [0] * (n + 1)
        for c in citations:
            counts[min(n, c)] += 1
        acc = 0
        for i in range(n, -1, -1):
            acc += counts[i]
            if acc >= i:
                return i
        return 0

'''
One-line
'''
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        return sum(i < j for i, j in enumerate(sorted(citations, reverse=True)))
{{< / highlight >}}
</div>

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
