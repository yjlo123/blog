---
weight: 167
title: "167 Two Sum II - Input array is sorted"
date: 2021-09-18T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_two_pointers"]
---
Given an array of integers `numbers` that is already _**sorted in non-decreasing order**_, find two numbers such that they add up to a specific `target` number.

Return _the indices of the two numbers (1-indexed) as an integer array_ `answer` _of size_ `2`_, where_ `1 <= answer[0] < answer[1] <= numbers.length`.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.


**Example 1:**
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```
**Example 2:**
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
```
**Example 3:**
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
```

**Constraints:**
- 2 <= numbers.length <= 3 * 10<sup>4</sup>
- -1000 <= numbers[i] <= 1000
- numbers is sorted in **non-decreasing order**.
- -1000 <= target <= 1000
- The tests are generated such that there is **exactly one solution**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        i = 0
        j = len(numbers) - 1
        while i < j:
            s = numbers[i] + numbers[j]
            if s == target:
                break
            elif s > target:
                j -= 1
            else:
                i += 1
        return [i + 1, j + 1]
{{< / highlight >}}
</div>
</div>
