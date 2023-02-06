---
weight: 1171
title: "1171 Remove Zero Sum Consecutive Nodes from Linked List"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.


(Note that in the examples below, all sequences are serializations of `ListNode` objects.)

**Example 1:**
```
Input: head = [1,2,-3,3,1]
Output: [3,1]
Note: The answer [1,2,1] would also be accepted.
```
**Example 2:**
```
Input: head = [1,2,3,-3,4]
Output: [1,2,4]
```
**Example 3:**
```
Input: head = [1,2,3,-3,-2]
Output: [1]
```

**Constraints:**
- The given linked list will contain between `1` and `1000` nodes.
- Each node in the linked list has `-1000 <= node.val <= 1000`.

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
    def removeZeroSumSublists(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        sum_set = set([0])
        sum_stack = [(dummy, 0)]

        current = dummy
        while current:
            cur_sum = sum_stack[-1][1] + current.val
            if cur_sum in sum_set:
                while sum_stack[-1][1] != cur_sum:
                    sum_set.remove(sum_stack.pop()[1])
                sum_stack[-1][0].next = current.next
            else:
                sum_set.add(cur_sum)
                sum_stack.append((current, cur_sum))
            current = current.next
        return dummy.next
{{< / highlight >}}
</div>
</div>
