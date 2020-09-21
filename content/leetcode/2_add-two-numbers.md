---
title: "2 Add Two Number"
date: 2019-02-16T01:17:33+08:00
draft: false
tags: ["leetcode"]
---

```
package main

import (
	"fmt"
)

type ListNode struct {
	Val  int
	Next *ListNode
}

type intArr []int

func (list *ListNode) toArr() []int {
	if list == nil {
		return []int{}
	}
	head := list
	var s []int
	for head != nil {
		s = append(s, head.Val)
		head = head.Next
	}
	return s
}

func (nums intArr) toList() *ListNode {
	if len(nums) == 0 {
		return nil
	}
	var head *ListNode = nil
	length := len(nums)
	for i, _ := range nums {
		num := nums[length-i-1]
		head = &ListNode{num, head}
	}
	return head
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

func main() {
	nums1 := intArr{2, 4, 3}
	nums2 := intArr{5, 6, 4}

	result := addTwoNumbers(nums1.toList(), nums2.toList())
	fmt.Println(result.toArr())
}
```