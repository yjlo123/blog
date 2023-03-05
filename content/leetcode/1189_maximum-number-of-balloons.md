---
weight: 1189
title: "1189 Maximum Number of Balloons"
date: 2023-03-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_hash_table"]
---

Given a string `text`, you want to use the characters of `text` to form as many instances of the word "**balloon**" as possible.

You can use each character in `text` **at most once**. Return the maximum number of instances that can be formed.


**Example 1:**
```
nlaebolko
nla bol o

Input: text = "nlaebolko"
Output: 1
```
**Example 2:**
```
loonbalxballpoon
loonbal
        ball oon

Input: text = "loonbalxballpoon"
Output: 2
```
**Example 3:**
```
Input: text = "leetcode"
Output: 0
```

**Constraints:**
- <code>1 <= text.length <= 10<sup>4</sup></code>
- `text` consists of lower case English letters only.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        counter = {'b':0, 'a':0, 'l':0, 'o':0, 'n':0}
        for char in text:
            if char in counter:
                counter[char] += 1

        counter['l'] //= 2
        counter['o'] //= 2
        return min(counter.values())
{{< / highlight >}}
</div>
</div>
