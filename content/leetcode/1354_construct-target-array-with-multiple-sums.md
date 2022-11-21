---
weight: 1354
title: "1354 Construct Target Array With Multiple Sums"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_heap"]
---

You are given an array `target` of n integers. From a starting array `arr` consisting of `n` 1's, you may perform the following procedure :

- let `x` be the sum of all elements currently in your array.
- choose index `i`, such that `0 <= i < n` and set the value of `arr` at index `i` to `x`.
- You may repeat this procedure as many times as needed.

Return _`true` if it is possible to construct the `target` array from arr, otherwise, return `false`_.


**Example 1:**
```
Input: target = [9,3,5]
Output: true
Explanation: Start with arr = [1, 1, 1] 
[1, 1, 1], sum = 3 choose index 1
[1, 3, 1], sum = 5 choose index 2
[1, 3, 5], sum = 9 choose index 0
[9, 3, 5] Done
```
**Example 2:**
```
Input: target = [1,1,1,2]
Output: false
Explanation: Impossible to create target array from [1,1,1,1].
```
**Example 3:**
```
Input: target = [8,5]
Output: true
```

**Constraints:**
- `n == target.length`
- <code>1 <= n <= 5 * 10<sup>4</sup></code>
- <code>1 <= target[i] <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
import heapq

class Solution:
    def isPossible(self, target: List[int]) -> bool:
        if len(target) == 1:
            return target == [1]
        
        total = sum(target)

        heap = [-num for num in target]
        heapq.heapify(heap)
        
        while -heap[0] > 1:
            largest = -heap[0]
            rest = total - largest
            if rest == 1:
                # only possible when n=2
                return True
            
            # since the largest was updated every time
            # this is fater than deducting by rest repeatedly
            x = largest % rest
            
            if x == 0 or x == largest:
                return False
            
            # same as pop and push new min, but faster
            heapq.heapreplace(heap, -x)
            total = total - largest + x

        return True
{{< / highlight >}}
</div>
</div>
