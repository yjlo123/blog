---
weight: 95
title: "95 Unique Binary Search Trees II"
date: 2022-12-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree", "lc_bst"]
---

Given an integer `n_`, return all the structurally unique **BST**'s (binary search trees), which has exactly `n` nodes of unique values from `1` to `n`_. Return the answer in **any order**.

**Example 1:**
```
1     1           2         3       3
 \     \         / \       /       /
  3     2       1   3     2       1
 /       \               /         \
2         3             1           2

Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```

**Example 2:**
```
Input: n = 1
Output: [[1]]
```

**Constraints:**
- `1 <= n <= 8`

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
    def build_tree(self, lo: int, hi: int) -> List[Optional[TreeNode]]:
        if lo > hi:
            return [None]
        trees = []
        for v in range(lo, hi+1):
            for l in self.build_tree(lo, v-1):
                for r in self.build_tree(v+1, hi):
                    trees.append(TreeNode(v, l, r))
        return trees

    def generateTrees(self, n: int) -> List[Optional[TreeNode]]:
        return self.build_tree(1, n)
{{< / highlight >}}
</div>
</div>
