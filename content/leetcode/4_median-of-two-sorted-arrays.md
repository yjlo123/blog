---
weight: 4
title: "4 Median of Two Sorted Arrays"
date: 2020-10-24T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_hard"]
---

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

**Follow up**: The overall run time complexity should be `O(log (m+n))`.

 

**Example 1:**
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

**Example 2:**
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

**Example 3:**
```
Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
```

**Example 4:**
```
Input: nums1 = [], nums2 = [1]
Output: 1.00000
```

**Example 5:**
```
Input: nums1 = [2], nums2 = []
Output: 2.00000
```

**Constraints:**

- nums1.length == m
- nums2.length == n
- 0 <= m <= 1000
- 0 <= n <= 1000
- 1 <= m + n <= 2000
- -10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
    m := len(nums1)
    n := len(nums2)
    if m > n {
        nums1, nums2 = nums2, nums1
        m, n = n, m
    }
    iMin := 0
    iMax := m
    halfLen := (m + n + 1) / 2
    for iMin <= iMax {
        i := (iMin + iMax) / 2
        j := halfLen - i
        if i < iMax && nums2[j-1] > nums1[i] {
            iMin = i + 1
        } else if i > iMin && nums1[i-1] > nums2[j] {
            iMax = i - 1
        } else {
            maxLeft := 0
            if i == 0 {
                maxLeft = nums2[j-1]
            } else if j == 0 {
                maxLeft = nums1[i-1]
            } else {
                maxLeft = Max(nums1[i-1], nums2[j-1])
            }
            if (m+n)%2 == 1 {
                return float64(maxLeft)
            }

            minRight := 0
            if i == m {
                minRight = nums2[j]
            } else if j == n {
                minRight = nums1[i]
            } else {
                minRight = Min(nums2[j], nums1[i])
            }
            return float64(maxLeft+minRight) / 2.0
        }
    }
    return 0.0
}
{{< / highlight >}}
</div>
</div>
