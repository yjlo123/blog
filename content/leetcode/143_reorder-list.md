---
weight: 143
title: "143 Reorder List"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

You are given the head of a singly linked-list. The list can be represented as:  
<code>L<sub>0</sub> → L<sub>1</sub> → … → L<sub>n - 1</sub> → L<sub>n</sub></code>  
_Reorder the list to be on the following form:_  
<code>L<sub>0</sub> → L<sub>n</sub> → L<sub>1</sub> → L<sub>n - 1</sub> → L<sub>2</sub> → L<sub>n - 2</sub> → …</code>  
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1:**
```
1 -> 2 -> 3 -> 4
       v
1 -> 4 -> 2 -> 3

Input: head = [1,2,3,4]
Output: [1,4,2,3]
```
**Example 2:**
```
1 -> 2 -> 3 -> 4 -> 5
          v
1 -> 5 -> 2 -> 4 -> 3

Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

**Constraints:**
- The number of nodes in the list is in the range <code>[1, 5 * 10<sup>4</sup>]</code>.
- `1 <= Node.val <= 1000`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def reorderList(self, head: ListNode) -> None:
        if not head:
            return 
        
        # find the middle of linked list [Problem 876]
        # in 1->2->3->4->5->6 find 4 
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next 
            
        # reverse the second part of the list [Problem 206]
        # convert 1->2->3->4->5->6 into 1->2->3->4 and 6->5->4
        # reverse the second half in-place
        prev, curr = None, slow
        while curr:
            curr.next, prev, curr = prev, curr, curr.next       

        # merge two sorted linked lists [Problem 21]
        # merge 1->2->3->4 and 6->5->4 into 1->6->2->5->3->4
        first, second = head, prev
        while second.next:
            first.next, first = second, first.next
            second.next, second = first, second.next


'''
Using recursion
'''
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        prev = slow = fast = head
        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next

        prev.next = None
        last, rev_head = self.reverseList(slow)
        last.next = None
        self.mergeList(head, rev_head)

    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None, None
        if not head.next:
            return head, head
        last, new_head = self.reverseList(head.next)
        last.next = head
        return head, new_head
    
    def mergeList(
        self,
        l1: Optional[ListNode],
        l2: Optional[ListNode]
    ) -> Optional[ListNode]:
        if not l1:
            return l2
        if not l2:
            return l1
        l1.next, l2.next = l2, self.mergeList(l1.next, l2.next)
        return l1
{{< / highlight >}}
</div>
</div>
