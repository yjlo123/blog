---
weight: 255
title: "255 Verify Preorder Sequence in Binary Search Tree"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_tree"]
---

Given an array of **unique** integers `preorder`, return _`true` if it is the correct preorder traversal sequence of a binary search tree_.

**Example 1:**
```
    5
   / \
  2   6
 / \
1   3

Input: preorder = [5,2,1,3,6]
Output: true
```
**Example 2:**
```
Input: preorder = [5,2,6,1,3]
Output: false
```

**Constraints:**
- <code>1 <= preorder.length <= 10<sup>4</sup></code>
- <code>1 <= preorder[i] <= 10<sup>4</sup></code>
- All the elements of `preorder` are **unique**.
 

**Follow up**: Could you do it using only constant space complexity?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def verifyPreorder(self, preorder: List[int]) -> bool:
        stack = []
        low = -math.inf
        for num in preorder:
            if num < low:
                return False
            while stack and num > stack[-1]:
                low = stack.pop()
            stack.append(num)
        return True


'''
O(1) space
Use the preoder list as the stack
'''
class Solution:
    def verifyPreorder(self, preorder: List[int]) -> bool:
        i = 0
        low = -math.inf
        for num in preorder:
            if num < low:
                return False
            while i > 0 and num > preorder[i - 1]:
                low = preorder[i - 1]
                i -= 1
            preorder[i] = num
            i += 1
        return True
{{< / highlight >}}
</div>
</div>
