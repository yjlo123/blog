---
weight: 659
title: "659 Split Array into Consecutive Subsequences"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_array", "lc_greedy"]
---

You are given an integer array `nums` that is **sorted in non-decreasing order**.

Determine if it is possible to split `nums` into **one or more subsequences** such that **both** of the following conditions are true:

- Each subsequence is a **consecutive increasing sequence** (i.e. each integer is **exactly one** more than the previous integer).
- All subsequences have a length of `3` **or more**.

Return _`true` if you can split `nums` according to the above conditions, or `false` otherwise_.

A **subsequence** of an array is a new array that is formed from the original array by deleting some (can be none) of the elements without disturbing the relative positions of the remaining elements. (i.e., `[1,3,5]` is a subsequence of <code>[<u>1</u>,2,<u>3</u>,4,<u>5</u>]</code> while `[1,3,2]` is not).


**Example 1:**
```
Input: nums = [1,2,3,3,4,5]
Output: true
Explanation: nums can be split into the following subsequences:
[1,2,3,3,4,5] --> 1, 2, 3
[1,2,3,3,4,5] --> 3, 4, 5
```
**Example 2:**
```
Input: nums = [1,2,3,3,4,4,5,5]
Output: true
Explanation: nums can be split into the following subsequences:
[1,2,3,3,4,4,5,5] --> 1, 2, 3, 4, 5
[1,2,3,3,4,4,5,5] --> 3, 4, 5
```
**Example 3:**
```
Input: nums = [1,2,3,4,4,5]
Output: false
Explanation: It is impossible to split nums into consecutive increasing
subsequences of length 3 or more.
```

**Constraints:**
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- `-1000 <= nums[i] <= 1000`
- `nums` is sorted in **non-decreasing** order.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def isPossible(self, nums: List[int]) -> bool:
        freq = defaultdict(int)
        need = defaultdict(int)
        for v in nums:
            freq[v] += 1
        
        for v in nums:
            if freq[v] == 0:
                # used in other seq
                continue
            if need[v] > 0:
                # can be added to a previous seq
                freq[v] -= 1
                need[v] -= 1
                need[v + 1] += 1
            elif freq[v] > 0 and freq[v+1] > 0 and freq[v+2] > 0:
                # as a start of a new seq
                freq[v] -= 1
                freq[v + 1] -= 1
                freq[v + 2] -= 1
                need[v + 3] += 1
            else:
                return False
        return True
{{< / highlight >}}
</div>
</div>
