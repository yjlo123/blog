---
weight: 2055
title: "2055 Plates Between Candles"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_binary_search", "lc_string"]
---

There is a long table with a line of plates and candles arranged on top of it. You are given a **0-indexed** string s consisting of characters `'*'` and `'|'` only, where a `'*'` represents a **plate** and a `'|'` represents a **candle**.

You are also given a **0-indexed** 2D integer array `queries` where <code>queries[i] = [left<sub>i</sub>, right<sub>i</sub>]</code> denotes the **substring** <code>s[left<sub>i</sub>...right<sub>i</sub>]</code> (**inclusive**). For each query, you need to find the **number** of plates **between candles** that are **in the substring**. A plate is considered **between candles** if there is at least one candle to its left **and** at least one candle to its right **in the substring**.

- For example, `s = "||**||**|*"`, and a query `[3, 8]` denotes the substring `"*||**|"`. The number of plates between candles in this substring is `2`, as each of the two plates has at least one candle **in the substring** to its left **and** right.

Return _an integer array `answer` where `answer[i]` is the answer to the <code>i<sup>th</sup></code> query._

**Example 1:**
```
                0 1 2 3 4 5 6 7 8 9
            s:  * * | * * | * * * |
queries[0] = [2,5]: | * * |
      queries[1] = [5,9]: | * * * |

Input: s = "**|**|***|", queries = [[2,5],[5,9]]
Output: [2,3]
Explanation:
- queries[0] has two plates between candles.
- queries[1] has three plates between candles.
```
**Example 2:**
```
                                       1 1 1 1 1 1 1 1 1 1 2
                   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0
            s:     * * * | * * | * * * * * | * * | | * * | *
queries[0] = [1,17]: * * | * * | * * * * * | * * | | *
       queries[1] = [4,5]: * *
                         queries[2] = [14,17]: * | | *
        queries[3] = [5,11]: * | * * * * *
                            ueries[4] = [15,16]: | |

Input: s = "***|**|*****|**||**|*", queries = [[1,17],[4,5],[14,17],[5,11],[15,16]]
Output: [9,0,0,0,0]
Explanation:
- queries[0] has nine plates between candles.
- The other queries have zero plates between candles.
```

**Constraints:**
- <code>3 <= s.length <= 10<sup>5</sup></code>
- `s` consists of `'*'` and `'|'` characters.
- <code>1 <= queries.length <= 10<sup>5</sup></code>
- `queries[i].length == 2`
- <code>0 <= left<sub>i</sub> <= right<sub>i</sub> < s.length</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def platesBetweenCandles(
        self,
        s: str,
        queries: List[List[int]]
    ) -> List[int]:
        A = [i for i,c in enumerate(s) if c == '|']
        res = []
        for a,b in queries:
            i = bisect.bisect_left(A, a)
            j = bisect.bisect(A, b) - 1
            res.append((A[j] - A[i]) - (j - i) if i < j else 0)
        return res
{{< / highlight >}}
</div>
</div>
