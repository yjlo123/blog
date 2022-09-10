---
weight: 2
title: "2 Add Two Numbers"
date: 2020-09-21T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**
```
(2 -> 4 -> 3) + (5 -> 6 -> 4)
= (7 -> 0 -> 8)
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**
```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:**
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

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
    def addTwoNumbers(
        self,
        l1: Optional[ListNode],
        l2: Optional[ListNode]
    ) -> Optional[ListNode]:
        dummy = ListNode(0)
        tail = dummy
        carry = 0
        while l1 or l2:
            num1 = l1.val if l1 else 0
            num2 = l2.val if l2 else 0
            s = num1 + num2 + carry
            carry = s // 10
            tail.next = ListNode(s % 10)
            tail = tail.next
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
        if carry:
            tail.next = ListNode(carry)
        return dummy.next
{{< / highlight >}}
</div>

<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
type ListNode struct {
    Val  int
    Next *ListNode
}

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    head := &ListNode{0, nil}
    result := head
    carry := 0
    for l1 != nil || l2 != nil {
        temp := carry
        if l1 != nil && l2 != nil {
            temp += l1.Val + l2.Val
        } else if l1 != nil {
            temp += l1.Val
        } else {
            temp += l2.Val
        }
        head.Next = &ListNode{temp % 10, nil}
        carry = temp / 10
        if l1 != nil {
            l1 = l1.Next
        }
        if l2 != nil {
            l2 = l2.Next
        }
        head = head.Next
    }
    if carry > 0 {
        head.Next = &ListNode{carry, nil}
    }
    return result.Next
}

{{< / highlight >}}
</div>

</div>
