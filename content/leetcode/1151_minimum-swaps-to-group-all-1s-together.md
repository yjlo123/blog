---
weight: 1151
title: "1151 Minimum Swaps to Group All 1's Together"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_sliding_window"]
---

Given a binary array `data`, return the minimum number of swaps required to group all `1`’s present in the array together in **any place** in the array.

**Example 1:**
```
Input: data = [1,0,1,0,1]
Output: 1
Explanation: There are 3 ways to group all 1's together:
[1,1,1,0,0] using 1 swap.
[0,1,1,1,0] using 2 swaps.
[0,0,1,1,1] using 1 swap.
The minimum is 1.
```
**Example 2:**
```
Input: data = [0,0,0,1,0]
Output: 0
Explanation: Since there is only one 1 in the array, no swaps are needed.
```
**Example 3:**
```
Input: data = [1,0,1,0,1,0,0,1,1,0,1]
Output: 3
Explanation: One possible solution that uses 3 swaps is [0,0,0,0,0,1,1,1,1,1,1].
```

**Constraints:**
- <code>1 <= data.length <= 10<sup>5</sup></code>
- `data[i]` is either `0` or `1`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minSwaps(self, data: List[int]) -> int:
        ones = sum(data)
        count, max_one = 0, 0
        l = r = 0
        while r < len(data):
            count += data[r]
            r += 1
            if r - l > ones:
                count -= data[l]
                l += 1
            max_one = max(max_one, count)
        return ones - max_one
{{< / highlight >}}
</div>
</div>
