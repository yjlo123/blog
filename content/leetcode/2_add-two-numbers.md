---
weight: 2
title: "2 Add Two Numbers"
date: 2020-09-21T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
<div class="tabs">
  <div class="tab-btn tab-btn-active" onclick="showLang(event, 'golang')">Golang</div>
</div>
<div class="tab-content">
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
