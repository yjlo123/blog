---
weight: 445
title: "445 Add Two Numbers II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**
```
 7 -> 2 -> 4 -> 3
      5 -> 6 -> 4
__________________
 7 -> 8 -> 0 -> 7

Input: l1 = [7,2,4,3], l2 = [5,6,4]
Output: [7,8,0,7]
```
**Example 2:**
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [8,0,7]
```
**Example 3:**
```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Constraints:**
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

**Follow up:** Could you solve it without reversing the input lists?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        def reverse_list(head):
            last = None
            while head:
                temp_next = head.next
                head.next = last
                last = head
                head = temp_next
            return last
            
        rev_l1 = reverse_list(l1)
        rev_l2 = reverse_list(l2)
        
        sum_head = None
        curry = 0
        while rev_l1 or rev_l2:
            v1 = rev_l1.val if rev_l1 else 0
            v2 = rev_l2.val if rev_l2 else 0
            val = curry + v1 + v2
            curry = val // 10
            val %= 10
            sum_head = ListNode(val, sum_head)
            rev_l1 = rev_l1.next if rev_l1 else None
            rev_l2 = rev_l2.next if rev_l2 else None
        
        if curry:
            sum_head = ListNode(curry, sum_head)
        return sum_head


'''
Without reversing list
'''
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        # find the length of both lists
        n1 = n2 = 0
        curr1, curr2 = l1, l2
        while curr1:
            curr1 = curr1.next 
            n1 += 1
        while curr2:
            curr2 = curr2.next 
            n2 += 1
            
        # parse both lists
        # and sum the corresponding positions 
        # without taking carry into account
        # 3->3->3 + 7->7 --> 3->10->10 --> 10->10->3
        curr1, curr2 = l1, l2
        head = None
        while n1 > 0 and n2 > 0:
            val = 0
            if n1 >= n2:
                val += curr1.val 
                curr1 = curr1.next 
                n1 -= 1
            if n1 < n2:
                val += curr2.val 
                curr2 = curr2.next
                n2 -= 1
                
            # update the result: add to front
            curr = ListNode(val)
            curr.next = head
            head = curr

        # take the carry into account
        # to have all elements to be less than 10
        # 10->10->3 --> 0->1->4 --> 4->1->0
        curr1, head = head, None
        carry = 0
        while curr1:
            # current sum and carry
            val = (curr1.val + carry) % 10
            carry = (curr1.val + carry) // 10
            
            # update the result: add to front
            curr = ListNode(val)
            curr.next = head
            head = curr

            # move to the next elements in the list
            curr1 = curr1.next
        
        # add the last carry
        if carry:
            curr = ListNode(carry)
            curr.next = head
            head = curr

        return head
{{< / highlight >}}
</div>
</div>
