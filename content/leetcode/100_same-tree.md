---
weight: 100
title: "100 Same Tree"
date: 2021-06-09T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_tree"]
---

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**
```
   1        1
  / \      / \
 2   3    2   3
Input: p = [1,2,3], q = [1,2,3]
Output: true
```

**Example 2:**
```
   1      1
  /        \
 2          2
Input: p = [1,2], q = [1,null,2]
Output: false
```
**Example 3:**
```
   1        1
  / \      / \
 2   1    1   2
Input: p = [1,2,1], q = [1,1,2]
Output: false
```

**Constraints:**

- The number of nodes in both trees is in the range `[0, 100]`.
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSameTree(p *TreeNode, q *TreeNode) bool {
    if p == nil || q == nil {
        return p == q
    }
    if p.Val != q.Val {
        return false
    }
    return isSameTree(p.Left, q.Left) && isSameTree(p.Right, q.Right)
}

{{< / highlight >}}
</div>
</div>
