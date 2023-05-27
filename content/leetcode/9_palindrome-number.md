---
weight: 9
title: "9 Palindrome Number"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_math"]
---

Given an integer `x`, return *`true` if `x` is a palindrome, and `false` otherwise*.

> palindrome: An integer is a **palindrome** when it reads the same forward and backward. For example, `121` is a palindrome while `123` is not.

**Example 1:**
```
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```
**Example 2:**
```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-.
Therefore it is not a palindrome.
```
**Example 3:**
```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Constraints:**
- <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>
 

**Follow up**: Could you solve it without converting the integer to a string?

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def isPalindrome(self, x: int) -> bool:
        rev = 0
        y = x
        while y > 0:
            rev = rev * 10 + y % 10
            y //= 10
        return rev == x


'''
Reverse only half
'''
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x % 10 == 0 and x != 0):
            return False
        
        rev = 0
        while x > rev:
            rev = rev * 10 + x % 10
            x //= 10
        
        return x == rev or x == rev // 10
{{< / highlight >}}
</div>
<div id="golang" class="lang">
{{< highlight golang "linenos=table" >}}
func isPalindrome(x int) bool {
    if x < 0 || (x % 10 == 0 && x != 0) {
        return false
    }

    revNum := 0
    for x > revNum {
        revNum = revNum * 10 + x % 10
        x /= 10
    }
    return x == revNum || x == revNum/10
}
{{< / highlight >}}
</div>
<div id="java" class="lang">
{{< highlight java "linenos=table" >}}
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }

        int reverted = 0;
        while (x > reverted) {
            reverted = reverted * 10 + x % 10;
            x /= 10;
        }

        return x == reverted || x == reverted / 10;
    }
}
{{< / highlight >}}
</div>
</div>
