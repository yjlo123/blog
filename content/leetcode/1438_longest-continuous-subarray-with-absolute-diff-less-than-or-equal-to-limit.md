---
weight: 1438
title: "1438 Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_queue", "lc_heap", "lc_sliding_window", "lc_array"]
---

Given an array of integers `nums` and an integer `limit`, return the size of the longest **non-empty** subarray such that the absolute difference between any two elements of this subarray is less than or equal to `limit`.

**Example 1:**
```
Input: nums = [8,2,4,7], limit = 4
Output: 2 
Explanation: All subarrays are: 
[8] with maximum absolute diff |8-8| = 0 <= 4.
[8,2] with maximum absolute diff |8-2| = 6 > 4. 
[8,2,4] with maximum absolute diff |8-2| = 6 > 4.
[8,2,4,7] with maximum absolute diff |8-2| = 6 > 4.
[2] with maximum absolute diff |2-2| = 0 <= 4.
[2,4] with maximum absolute diff |2-4| = 2 <= 4.
[2,4,7] with maximum absolute diff |2-7| = 5 > 4.
[4] with maximum absolute diff |4-4| = 0 <= 4.
[4,7] with maximum absolute diff |4-7| = 3 <= 4.
[7] with maximum absolute diff |7-7| = 0 <= 4. 
Therefore, the size of the longest subarray is 2.
```
**Example 2:**
```
Input: nums = [10,1,2,4,7,2], limit = 5
Output: 4 
Explanation: The subarray [2,4,7,2] is the longest
since the maximum absolute diff is |2-7| = 5 <= 5.
```
**Example 3:**
```
Input: nums = [4,2,2,2,4,4,2,2], limit = 0
Output: 3
```

**Constraints:**
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>1 <= nums[i] <= 10<sup>9</sup></code>
- <code>0 <= limit <= 10<sup>9</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import deque

class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        max_q = deque()
        min_q = deque()
        i = 0
        for a in nums:
            while max_q and a > max_q[-1]:
                max_q.pop()
            while min_q and a < min_q[-1]:
                min_q.pop()
            max_q.append(a)
            min_q.append(a)
            # max_q[0]-min_q[0] is the largest diff in the window A[i]...A[j]
            if max_q[0] - min_q[0] > limit:
                if max_q[0] == nums[i]:
                    max_q.popleft()
                if min_q[0] == nums[i]:
                    min_q.popleft()
                i += 1
        # we only need to max window size (j-i)
        return len(nums) - i


'''
Using min&max heaps
'''
import heapq

class Solution:
    def longestSubarray(self, nums, limit):
        max_q, min_q = [], []
        res = i = 0
        for j, a in enumerate(nums):
            heapq.heappush(max_q, [-a, j])
            heapq.heappush(min_q, [a, j])
            while -max_q[0][0] - min_q[0][0] > limit:
                i = min(max_q[0][1], min_q[0][1]) + 1
                while max_q[0][1] < i:
                    heapq.heappop(max_q)
                while min_q[0][1] < i:
                    heapq.heappop(min_q)
            res = max(res, j - i + 1)
        return res
{{< / highlight >}}
</div>
</div>
