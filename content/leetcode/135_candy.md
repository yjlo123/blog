---
weight: 135
title: "135 Candy"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_array"]
---

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:
- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.
Return _the minimum number of candies you need to have to distribute the candies to the children._

**Example 1:**
```
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first,
second and third child with 2, 1, 2 candies respectively.
```
**Example 2:**
```
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the first,
second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.
```

**Constraints:**
- `n == ratings.length`
- <code>1 <= n <= 2 * 10<sup>4</sup></code>
- <code>0 <= ratings[i] <= 2 * 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        arr = [1] * n
        for i in range(1, n):
            if ratings[i] > ratings[i-1]:
                arr[i] = arr[i-1] + 1
        s = arr[n-1]
        for i in range(n-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                arr[i] = max(arr[i], arr[i+1]+1)
            s += arr[i]
        return s
{{< / highlight >}}
</div>
</div>
