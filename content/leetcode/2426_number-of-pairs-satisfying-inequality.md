---
weight: 2426
title: "2426 Number of Pairs Satisfying Inequality"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_binary_search"]
---

You are given two **0-indexed** integer arrays `nums1` and `nums2`, each of size `n`, and an integer `diff`. Find the number of **pairs** `(i, j)` such that:

- `0 <= i < j <= n - 1` **and**
- `nums1[i] - nums1[j] <= nums2[i] - nums2[j] + diff`.
Return *the **number of pairs** that satisfy the conditions*.

**Example 1:**
```
Input: nums1 = [3,2,5], nums2 = [2,2,1], diff = 1
Output: 3
Explanation:
There are 3 pairs that satisfy the conditions:
1. i = 0, j = 1: 3 - 2 <= 2 - 2 + 1. Since i < j and 1 <= 1, this pair satisfies the conditions.
2. i = 0, j = 2: 3 - 5 <= 2 - 1 + 1. Since i < j and -2 <= 2, this pair satisfies the conditions.
3. i = 1, j = 2: 2 - 5 <= 2 - 1 + 1. Since i < j and -3 <= 2, this pair satisfies the conditions.
Therefore, we return 3.
```
**Example 2:**
```
Input: nums1 = [3,-1], nums2 = [-2,2], diff = -1
Output: 0
Explanation:
Since there does not exist any pair that satisfies the conditions, we return 0.
```

**Constraints:**
- `n == nums1.length == nums2.length`
- <code>2 <= n <= 10<sup>5</sup></code>
- <code>-10<sup>4</sup> <= nums1[i], nums2[i] <= 10<sup>4</sup></code>
- <code>-10<sup>4</sup> <= diff <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def numberOfPairs(self, nums1: List[int], nums2: List[int], diff: int) -> int:
        res = 0
        sorted_list = []
        for n1, n2 in zip(nums1, nums2):
            # nums1[i] - nums1[j] <= nums2[i] - nums2[j] + diff
            # (nums1[i] - nums2[i]) <= (nums1[j] - nums2[j]) + diff
            # find the number of i for each j
            res += bisect.bisect_right(sorted_list, n1 - n2 + diff)
            bisect.insort(sorted_list, n1 - n2)
        return res
{{< / highlight >}}
</div>
</div>
