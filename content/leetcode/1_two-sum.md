---
title: "1 Two Sum"
date: 2019-02-16T01:17:33+08:00
draft: false
tags: ["leetcode"]
---

```
package main

import (
	"fmt"
)

func twoSum(nums []int, target int) []int {
	d := make(map[int]int)
	for idx, num := range nums {
		if v, ok := d[num]; ok {
			return []int{v, idx}
		}
		d[target-num] = idx
	}
	return nil
}

func main() {
	arr := []int{2, 7, 11, 15}
	fmt.Println(twoSum(arr, 9))
}
```
