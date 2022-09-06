---
weight: 875
title: "875 Koko Eating Bananas"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_binary_search"]
---

Koko loves to eat bananas. There are `n` piles of bananas, the <code>i<sup>th</sup></code> pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return _the minimum integer `k` such that she can eat all the bananas within h hours._

**Example 1:**
```
Input: piles = [3,6,7,11], h = 8
Output: 4
```
**Example 2:**
```
Input: piles = [30,11,23,4,20], h = 5
Output: 30
```
**Example 3:**
```
Input: piles = [30,11,23,4,20], h = 6
Output: 23
```

**Constraints:**
- <code>1 <= piles.length <= 10<sup>4</sup></code>
- <code>piles.length <= h <= 10<sup>9</sup></code>
- <code>1 <= piles[i] <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        left = 1
        right = max(piles)
        
        while left < right:
            mid = left + (right - left) // 2
            hours = 0
            for p in piles:
                hours += math.ceil(p / mid)
            
            if hours <= h:
                right = mid
            else:
                left = mid + 1
        return right
{{< / highlight >}}
</div>
</div>
