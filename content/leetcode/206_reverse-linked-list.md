---
weight: 206
title: "206 Reverse Linked List"
date: 2021-10-02T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_linked_list"]
---
Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**
```
1 -> 2 -> 3 -> 4 -> 5
          |
          v
5 -> 4 -> 3 -> 2 -> 1

Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
**Example 2:**
```
1 -> 2
2 -> 1

Input: head = [1,2]
Output: [2,1]
```
**Example 3:**
```
Input: head = []
Output: []
 ```

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- -5000 <= `Node.val` <= 5000

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

''' Recursive '''
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        next_node = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return next_node

''' Iterative '''
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        while head:
            new_head = head.next
            head.next = prev
            prev = head
            head = new_head
        return prev
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight golang "linenos=table" >}}
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

 /* Recursive */
func reverseList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil{
        return head
    }
    newHead := reverseList(head.Next)
    head.Next.Next = head
    head.Next = nil
    return newHead
}

/* Iterative */
func reverseList(head *ListNode) *ListNode {
	var prev *ListNode
	nextHead := head
	for head != nil {
		nextHead = head.Next
		head.Next = prev
		prev = head
		head = nextHead
	}
	return prev
}
{{< / highlight >}}
</div>
</div>
