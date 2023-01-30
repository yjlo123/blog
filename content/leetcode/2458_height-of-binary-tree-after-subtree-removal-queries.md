---
weight: 2458
title: "2458 Height of Binary Tree After Subtree Removal Queries"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_tree", "lc_dfs"]
---

You are given the `root` of a **binary tree** with `n` nodes. Each node is assigned a unique value from `1` to `n`. You are also given an array `queries` of size `m`.

You have to perform `m` **independent** queries on the tree where in the <code>i<sup>th</sup></code> query you do the following:

- **Remove** the subtree rooted at the node with the value `queries[i]` from the tree. It is **guaranteed** that `queries[i]` will **not** be equal to the value of the root.

Return *an array `answer` of size `m` where `answer[i]` is the height of the tree after performing the <code>i<sup>th</sup></code> query*.

**Note:**
- The queries are independent, so the tree returns to its **initial** state after each query.
- The height of a tree is the **number of edges in the longest** simple path from the root to some node in the tree.

**Example 1:**
```
    1                  1
   / \                /
  3   4      ==>     3
 /   / \            /
2   6   5          2
         \
          7

Input: root = [1,3,4,2,null,6,5,null,null,null,null,null,7], queries = [4]
Output: [2]
Explanation: The diagram above shows the tree after removing the subtree rooted at node with value 4.
The height of the tree is 2 (The path 1 -> 3 -> 2).
```
**Example 2:**
```
        5
     /     \
    8       9
   / \     / \
  2   1   3   7
 / \
4   6

Input: root = [5,8,9,2,1,3,7,4,6], queries = [3,2,4,8]
Output: [3,2,3,2]
Explanation: We have the following queries:
- Removing the subtree rooted at node with value 3. The height of the tree becomes 3 (The path 5 -> 8 -> 2 -> 4).
- Removing the subtree rooted at node with value 2. The height of the tree becomes 2 (The path 5 -> 8 -> 1).
- Removing the subtree rooted at node with value 4. The height of the tree becomes 3 (The path 5 -> 8 -> 2 -> 6).
- Removing the subtree rooted at node with value 8. The height of the tree becomes 2 (The path 5 -> 9 -> 3).
```

**Constraints:**
- The number of nodes in the tree is `n`.
- <code>2 <= n <= 10<sup>5</sup></code>
- `1 <= Node.val <= n`
- All the values in the tree are **unique**.
- `m == queries.length`
- <code>1 <= m <= min(n, 10<sup>4</sup>)</code>
- `1 <= queries[i] <= n`
- `queries[i] != root.val`

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
    def treeQueries(self, root: Optional[TreeNode], queries: List[int]) -> List[int]:
        @cache
        def height(node):
            if not node:
                return 0
            return 1 + max(height(node.left), height(node.right))

        def dfs(node, depth, max_h):
            # `max_h` is the max height without considering
            #    the subtree rooted at `node`
            if not node:
                return
            self.ans[node.val] = max_h
            dfs(node.left, depth+1, max(max_h, depth+height(node.right)))
            dfs(node.right, depth+1, max(max_h, depth+height(node.left)))
        
        self.ans = {}
        dfs(root, 0, 0)
        print(self.ans)
        return [self.ans[q] for q in queries]
{{< / highlight >}}
</div>
</div>
