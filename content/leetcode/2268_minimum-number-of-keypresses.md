---
weight: 2268
title: "2268 Minimum Number of Keypresses"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_greedy"]
---

You have a keypad with 9 buttons, numbered from `1` to `9`, each mapped to lowercase English letters. You can choose which characters each button is matched to as long as:
- All 26 lowercase English letters are mapped to.
- Each character is mapped to by **exactly** 1 button.
- Each button maps to **at most** 3 characters.

To type the first character matched to a button, you press the button once. To type the second character, you press the button twice, and so on.

Given a string `s`, return _the **minimum** number of keypresses needed to type `s` using your keypad._

**Note** that the characters mapped to by each button, and the order they are mapped in cannot be changed.

**Example 1:**
```
  1     2     3
 abc   df    eij
  4     5     6
 gqs   lkx   ptu
  7     8     9
 mnr   hyz   ovw

Input: s = "apple"
Output: 5
Explanation: One optimal way to setup your keypad is shown above.
Type 'a' by pressing button 1 once.
Type 'p' by pressing button 6 once.
Type 'p' by pressing button 6 once.
Type 'l' by pressing button 5 once.
Type 'e' by pressing button 3 once.
A total of 5 button presses are needed, so return 5.
```
**Example 2:**
```
  1     2     3
 ajs   bkt   clu
  4     5     6
 dmv   enw   fox
  7     8     9
 gpy   hqz   ir

Input: s = "abcdefghijkl"
Output: 15
Explanation: One optimal way to setup your keypad is shown above.
The letters 'a' to 'i' can each be typed by pressing a button once.
Type 'j' by pressing button 1 twice.
Type 'k' by pressing button 2 twice.
Type 'l' by pressing button 3 twice.
A total of 15 button presses are needed, so return 15.
```

**Constraints:**
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minimumKeypresses(self, s: str) -> int:
        c = collections.Counter(s)
        sorted_c = sorted(c.values(), reverse=True)
        res = 0
        res += sum([v for v in sorted_c[:9]])
        res += sum([v * 2 for v in sorted_c[9:18]])
        res += sum([v * 3 for v in sorted_c[18:]])
        return res
{{< / highlight >}}
</div>
</div>
