---
weight: 350
title: "350 Intersection of Two Arrays II"
date: 2021-09-30T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array", "lc_hash_table"]
---

Given two integer arrays `nums1` and `nums2`, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in **any order**.

**Example 1:**
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```
**Example 2:**
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```

**Constraints:**
- 1 <= `nums1.length`, `nums2.length` <= 1000
- 0 <= `nums1[i]`, `nums2[i]` <= 1000

**Follow up:**
- What if the given array is already sorted? How would you optimize your algorithm?
- What if `nums1`'s size is small compared to `nums2`'s size? Which algorithm is better?
- What if elements of `nums2` are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        if len(nums1) > len(nums2):
            return self.intersect(nums2, nums1)

        m1 = {}
        for n in nums1:
            if n in m1:
                m1[n] += 1
            else:
                m1[n] = 1
        result = []
        for n in nums2:
            if n in m1 and m1[n] > 0:
                result.append(n)
                m1[n] -= 1
        return result
{{< / highlight >}}
</div>
</div>
