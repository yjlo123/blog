---
weight: 282
title: "282 Expression Add Operators"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_back_tracking"]
---

Given a string `num` that contains only digits and an integer `target`, return _**all possibilities** to insert the binary operators `'+'`, `'-'`, and/or `'*'` between the digits of `num` so that the resultant expression evaluates to the `target` value_.

Note that operands in the returned expressions **should not** contain leading zeros.

**Example 1:**
```
Input: num = "123", target = 6
Output: ["1*2*3","1+2+3"]
Explanation: Both "1*2*3" and "1+2+3" evaluate to 6.
```
**Example 2:**
```
Input: num = "232", target = 8
Output: ["2*3+2","2+3*2"]
Explanation: Both "2*3+2" and "2+3*2" evaluate to 8.
```
**Example 3:**
```
Input: num = "3456237490", target = 9191
Output: []
Explanation: There are no expressions that can be created from "3456237490" to evaluate to 9191.
```

**Constraints:**
- `1 <= num.length <= 10`
- `num` consists of only digits.
- <code>-2<sup>31</sup> <= target <= 2sup>31</sup> - 1</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def addOperators(self, num: str, target: int) -> List[str]:
        def backtrack(num: str, vals: List[int], exp: str):
            if num == '' and sum(vals) == target:
                result.append(exp)
                return

            if not num:
                return

            for i in range(1, len(num) + 1):
                if i > 1 and num[0] == '0':
                    break
                    
                cur_num = num[:i]
                cur_int = int(cur_num)

                if not vals:
                    # first num
                    backtrack(num[i:], [cur_int], cur_num)
                    continue

                backtrack(num[i:], vals+[cur_int], exp+'+'+cur_num)
                backtrack(num[i:], vals+[-cur_int], exp+'-'+cur_num)
                backtrack(num[i:], vals[:-1] + [vals[-1] * cur_int], exp+'*'+cur_num)

        result = []
        backtrack(num, [], '')
        return result
{{< / highlight >}}
</div>
</div>
