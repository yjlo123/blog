---
weight: 398
title: "398 Random Pick Index"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_random", "lc_hash_table"]
---

Given an integer array `nums` with possible duplicates, randomly output the index of a given `target` number. You can assume that the given target number must exist in the array.

Implement the `Solution` class:
- `Solution(int[] nums)` Initializes the object with the array `nums`.
- `int pick(int target)` Picks a random index `i` from `nums` where `nums[i] == target`. If there are multiple valid i's, then each index should have an equal probability of returning.


**Example 1:**
```
Input
["Solution", "pick", "pick", "pick"]
[[[1, 2, 3, 3, 3]], [3], [1], [3]]
Output
[null, 4, 0, 2]

Explanation
Solution solution = new Solution([1, 2, 3, 3, 3]);
solution.pick(3); // It should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(1); // It should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(3); // It should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
```

**Constraints:**
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>
- `target` is an integer from `nums`.
- At most <code>10<sup>4</sup></code> calls will be made to `pick`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:

    def __init__(self, nums: List[int]):
        self.data = collections.defaultdict(list)
        for i, v in enumerate(nums):
            self.data[v].append(i)

    def pick(self, target: int) -> int:
        return random.choice(self.data[target])


# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.pick(target)


'''
Reservoir sampling (TLE)
'''
class Solution:

    def __init__(self, nums: List[int]):
        self.data = nums

    def pick(self, target: int) -> int:
        count, idx = 0, 0
        for i in range(len(self.data)):
            if self.data[i] == target:
                count += 1
                if random.randint(0, count-1) == 0:
                    idx = i
        return idx
{{< / highlight >}}
</div>
</div>
