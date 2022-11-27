---
weight: 354
title: "354 Russian Doll Envelopes"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp", "lc_binary_search"]
---

You are given a 2D array of integers `envelopes` where <code>envelopes[i] = [w<sub>i</sub>, h<sub>i</sub>]</code> represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope are greater than the other envelope's width and height.

Return _the maximum number of envelopes you can Russian doll (i.e., put one inside the other)_.

**Note**: You cannot rotate an envelope.

**Example 1:**
```
Input: envelopes = [[5,4],[6,4],[6,7],[2,3]]
Output: 3
Explanation: The maximum number of envelopes you can Russian doll is 3
([2,3] => [5,4] => [6,7]).
```
**Example 2:**
```
Input: envelopes = [[1,1],[1,1],[1,1]]
Output: 1
```

**Constraints:**
- <code>1 <= envelopes.length <= 10<sup>5</sup></code>
- `envelopes[i].length == 2`
- <code>1 <= w<sub>i</sub>, h<sub>i</sub> <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from bisect import bisect_left

class Solution:
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:
        '''
        E.g.
         ---------------> incr
         1, 2, 5, 5, 6, 6
         8, 3, 4, 2, 7, 4
               --->  ---> decr
            ^  ^     ^    longest incr subseq
        '''
        envelopes.sort(key=lambda x: (x[0], -x[1]))
        dp = []
        '''
        dp is an array such that dp[i] is the smallest element that
        ends an increasing subsequence of length i + 1. Whenever we
        encounter a new element e, we binary search inside dp to find
        the largest index i such that e can end that subsequence. We
        then update dp[i] with e.

        The length of the LIS is the same as the length of dp, as if
        dp has an index i, then it must have a subsequence of length
        i+1.
        '''

        arr = [e[1] for e in envelopes]
        for num in arr:
            idx = bisect_left(dp, num)
            if idx == len(dp):
                dp.append(num)
            else:
                dp[idx] = num
        return len(dp)
{{< / highlight >}}
</div>
</div>
