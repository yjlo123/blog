---
weight: 1339
title: "1339 Maximum Product of Splitted Binary Tree"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_dfs"]
---

Given the `root` of a binary tree, split the binary tree into two subtrees by removing one edge such that the product of the sums of the subtrees is maximized.

Return the maximum product of the sums of the two subtrees. Since the answer may be too large, return it **modulo** <code>10<sup>9</sup> + 7</code>.

**Note** that you need to maximize the answer before taking the mod and not after taking it.


**Example 1:**
```
     1                1
    /  \               \
   /    \               \
  2      3  =>   2       3
 / \    /       / \     /
4   5  6       4   5   6
              sum=11  sum=10

Input: root = [1,2,3,4,5,6]
Output: 110
Explanation: Remove the red edge and get 2 binary trees with sum 11 and 10.
Their product is 110 (11*10)
```
**Example 2:**
```
1
 \              1
  2              \         4
 / \      =>      2       / \
3   4            /       5   6
   / \          3
  5   6        sum=6     sum=15

Input: root = [1,null,2,3,4,null,null,5,6]
Output: 90
Explanation: Remove the red edge and get 2 binary trees with sum 15 and 6.
Their product is 90 (15*6)
```

**Constraints:**
- The number of nodes in the tree is in the range <code>[2, 5 * 10<sup>4</sup>]</code>.
- <code>1 <= Node.val <= 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:

    def maxProduct(self, root: Optional[TreeNode]) -> int:
        all_sums = []

        def tree_sum(subroot):
            if subroot is None: return 0
            left_sum = tree_sum(subroot.left)
            right_sum = tree_sum(subroot.right)
            total_sum = left_sum + right_sum + subroot.val
            all_sums.append(total_sum)
            return total_sum

        total = tree_sum(root)
        best = 0
        for s in all_sums:
            best = max(best, s * (total - s))   
        return best % (10 ** 9 + 7)
{{< / highlight >}}
</div>
</div>
