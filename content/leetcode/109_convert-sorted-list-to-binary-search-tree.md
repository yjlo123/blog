---
weight: 109
title: "109 Convert Sorted List to Binary Search Tree"
date: 2021-03-21T00:00:00+08:00
draft: ffalsse
tags: ["leetcode",  "lc_medium", "lc_tree"]
---

Given the `head` of a singly linked list where elements are **sorted in ascending order**, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of _every_ node never differ by more than 1.

**Example 1:**
```
-10 -> -3 -> 0 -> 5 -> 9

       0                   0
     /   \               /   \
   -10    5      or    -3     9
     \     \           /     /
     -3     9        -10    5

Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5],
which represents the shown height balanced BST.
```
**Example 2:**
```
Input: head = []
Output: []
```
**Example 3:**
```
Input: head = [0]
Output: [0]
```
**Example 4:**
```
Input: head = [1,3]
Output: [3,1]
```

**Constraints:**

- The number of nodes in head is in the range [0, 2 * 104].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:

    def findSize(self, head):
        ptr = head
        c = 0
        while ptr:
            ptr = ptr.next
            c += 1
        return c


    def sortedListToBST(self, head: ListNode) -> TreeNode:
        # Get the size of the linked list first
        size = self.findSize(head)

        # Recursively form a BST out of linked list from l --> r
        def convert(l, r):
            nonlocal head

            # Invalid case
            if l > r:
                return None

            mid = (l + r) // 2

            # First step of simulated inorder traversal. Recursively form
            # the left half
            left = convert(l, mid - 1)

            # Once left half is traversed, process the current node
            node = TreeNode(head.val)   
            node.left = left

            # Maintain the invariance mentioned in the algorithm
            head = head.next

            # Recurse on the right hand side and form BST out of them
            node.right = convert(mid + 1, r)
            return node
        return convert(0, size - 1)
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findSize(head *ListNode) int {
	c := 0
	for head != nil {
		head = head.Next
		c++
	}
	return c
}

var list *ListNode

func convert(left, right int) *TreeNode {
	if left > right {
		return nil
	}

	mid := (left + right) / 2
	newLeft := convert(left, mid-1)
	node := &TreeNode{list.Val, newLeft, nil}

	list = list.Next
	node.Right = convert(mid+1, right)
	return node
}

func sortedListToBST(head *ListNode) *TreeNode {
	list = head
	size := findSize(head)
	return convert(0, size-1)
}
{{< / highlight >}}
</div>

</div>
