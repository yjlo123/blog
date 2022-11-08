---
weight: 888
title: "888 Fair Candy Swap"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

Alice and Bob have a different total number of candies. You are given two integer arrays `aliceSizes` and `bobSizes` where `aliceSizes[i]` is the number of candies of the <code>i<sup>th</sup></code> box of candy that Alice has and `bobSizes[j]` is the number of candies of the <code>j<sup>th</sup></code> box of candy that Bob has.

Since they are friends, they would like to exchange one candy box each so that after the exchange, they both have the same total amount of candy. The total amount of candy a person has is the sum of the number of candies in each box they have.

Return _an integer array `answer` where `answer[0]` is the number of candies in the box that Alice must exchange, and `answer[1]` is the number of candies in the box that Bob must exchange_. If there are multiple answers, you may **return any** one of them. It is guaranteed that at least one answer exists.

**Example 1:**
```
Input: aliceSizes = [1,1], bobSizes = [2,2]
Output: [1,2]
```
**Example 2:**
```
Input: aliceSizes = [1,2], bobSizes = [2,3]
Output: [1,2]
```
**Example 3:**
```
Input: aliceSizes = [2], bobSizes = [1,3]
Output: [2,3]
```

**Constraints:**
- <code>1 <= aliceSizes.length, bobSizes.length <= 10<sup>4</sup></code>
- <code>1 <= aliceSizes[i], bobSizes[j] <= 10<sup>5</sup></code>
- Alice and Bob have a different total number of candies.
- There will be at least one valid answer for the given input.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def fairCandySwap(
        self,
        aliceSizes: List[int],
        bobSizes: List[int]
    ) -> List[int]:
        set2 = set(bobSizes)
        diff = (sum(aliceSizes) - sum(bobSizes)) // 2
        for c in aliceSizes:
            if c - diff in set2:
                return [c, c - diff]
        return []
{{< / highlight >}}
</div>
</div>
