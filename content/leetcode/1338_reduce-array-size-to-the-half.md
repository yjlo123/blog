---
weight: 1338
title: "1338 Reduce Array Size to The Half"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_hash_table"]
---

You are given an integer array `arr`. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return _the minimum size of the set so that **at least** half of the integers of the array are removed_.

**Example 1:**
```
Input: arr = [3,3,3,3,5,5,5,2,2,7]
Output: 2
Explanation: Choosing {3,7} will make the new array [5,5,5,2,2] which has size 5
(i.e equal to half of the size of the old array).
Possible sets of size 2 are {3,5},{3,2},{5,2}.
Choosing set {2,7} is not possible as it will make the new array [3,3,3,3,5,5,5]
which has a size greater than half of the size of the old array.
```
**Example 2:**
```
Input: arr = [7,7,7,7,7,7]
Output: 1
Explanation: The only possible set you can choose is {7}.
This will make the new array empty.
```

**Constraints:**
- <code>2 <= arr.length <= 10<sup>5</sup></code>
- `arr.length` is even.
- <code>1 <= arr[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minSetSize(self, arr: List[int]) -> int:
        counts = defaultdict(int)
        for num in arr:
            counts[num] += 1

        total_count = 0
        num_count = 0
        half_size = len(arr) // 2
        for count in sorted(counts.values(), reverse=True):
            total_count += count
            num_count += 1
            if total_count >= half_size:
                break
        return num_count
{{< / highlight >}}
</div>
</div>
