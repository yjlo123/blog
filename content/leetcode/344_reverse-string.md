---
weight: 344
title: "344 Reverse String"
date: 2020-10-20T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

You may assume all the characters consist of `printable ascii characters`.
  

**Example 1:**
```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**
```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

<div class="tabs"></div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func reverseString(s []byte]) {
	i , j := 0, len(s) - 1
	for i < j {
		temp := s[i]
		s[i] = s[j]
		i++
		s[j] = temp
		j--
	}
	fmt.Println(s)
}
{{< / highlight >}}
</div>

<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
public void reverseString(char[] s) {
    int i = 0;
    int j = s.length - 1;
    while (i < j) {
        char temp = s[i];
        s[i++] = s[j];
        s[j--] = temp;
    }
    System.out.println(s);
}
{{< / highlight >}}
</div>

<div id="runtime" class="lang">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode344" target="_blank">https://runtime.siwei.dev/?src=leetcode344</a>
    </div>
</div>
</div>