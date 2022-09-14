---
weight: 61
title: "61 Rotate List"
date: 2021-06-14T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_medium", "lc_linked_list"]
---

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**
```
          1 -> 2 -> 3 -> 4 -> 5
rotate 1: 5 -> 1 -> 2 -> 3 -> 4
rotate 2: 4 -> 5 -> 1 -> 2 -> 3

Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

**Example 2:**
```
          0 -> 1 -> 2
rotate 1: 2 -> 0 -> 1
rotate 2: 1 -> 2 -> 0
rotate 3: 0 -> 1 -> 2
rotate 4: 2 -> 0 -> 1

Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

**Constraints:**
- The number of nodes in the list is in the range `[0, 500]`.
- `-100 <= Node.val <= 100`
- <code>0 <= k <= 2 * 10<sup>9</sup></code>

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
    def rotateRight(
        self,
        head: Optional[ListNode],
        k: int
    ) -> Optional[ListNode]:
        if not head:
            return None
        
        length = 1
        tail = head
        while tail.next:
            tail = tail.next
            length += 1
        k = k % length
        
        tail.next = head
        if k > 0:
            for i in range(length - k):
                tail = tail.next

        new_head = tail.next
        tail.next = None
        return new_head
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
func rotateRight(head *ListNode, k int) *ListNode {
    if head == nil {
        return head
    }
    
    tail := head
    count := 1
    for tail.Next != nil {
        tail = tail.Next
        count++
    }
    
    tail.Next = head
    k %= count
    if k != 0 {
        for i := 0; i < count-k; i++ {
            tail = tail.Next
        }
    }
    
    newHead := tail.Next
    tail.Next = nil
    return newHead
}
{{< / highlight >}}
</div>
</div>
