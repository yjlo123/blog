---
weight: 2303
title: "2303 Calculate Amount Paid in Taxes"
date: 2022-11-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_easy", "lc_array"]
---

You are given a **0-indexed** 2D integer array `brackets` where <code>brackets[i] = [upper<sub>i</sub>, percent<sub>i</sub>]</code> means that the <code>i<sup>th</sup></code> tax bracket has an upper bound of upperi and is taxed at a rate of <code>percent<sub>i</sub></code>. The brackets are sorted by upper bound (i.e. <code>upper<sub>i-1</sub> < upper<sub>i</sub></code> for `0 < i < brackets.length`).

Tax is calculated as follows:
- The first <code>upper<sub>0</sub></code> dollars earned are taxed at a rate of <code>percent<sub>0</sub></code>.
- The next <code>upper<sub>1</sub> - upper<sub>0</sub></code> dollars earned are taxed at a rate of <code>percent<sub>1</sub></code>.
- The next <code>upper<sub>2</sub> - upper<sub>1</sub></code> dollars earned are taxed at a rate of <code>percent<sub>2</sub></code>.
- And so on.

You are given an integer `income` representing the amount of money you earned. Return the amount of money that you have to pay in taxes. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.


**Example 1:**
```
Input: brackets = [[3,50],[7,10],[12,25]], income = 10
Output: 2.65000
Explanation:
Based on your income, you have 3 dollars in the 1st tax bracket,
4 dollars in the 2nd tax bracket, and 3 dollars in the 3rd tax bracket.
The tax rate for the three tax brackets is 50%, 10%, and 25%, respectively.
In total, you pay $3 * 50% + $4 * 10% + $3 * 25% = $2.65 in taxes.
```
**Example 2:**
```
Input: brackets = [[1,0],[4,25],[5,50]], income = 2
Output: 0.25000
Explanation:
Based on your income, you have 1 dollar in the 1st tax bracket and 1 dollar
in the 2nd tax bracket.
The tax rate for the two tax brackets is 0% and 25%, respectively.
In total, you pay $1 * 0% + $1 * 25% = $0.25 in taxes.
```
**Example 3:**
```
Input: brackets = [[2,50]], income = 0
Output: 0.00000
Explanation:
You have no income to tax, so you have to pay a total of $0 in taxes.
```

**Constraints:**
- `1 <= brackets.length <= 100`
- <code>1 <= upper<sub>i</sub> <= 1000</code>
- <code>0 <= percent<sub>i</sub> <= 100</code>
- `0 <= income <= 1000`
- <code>upper<sub>i</sub></code> is sorted in ascending order.
- All the values of <code>upper<sub>i</sub></code> are unique.
- The upper bound of the last tax bracket is greater than or equal to `income`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def calculateTax(self, brackets: List[List[int]], income: int) -> float:
        res, prev = 0, 0
        for b, p in brackets:
            if not income:
                break
            t = min(income, b - prev)
            res += t * p / 100
            income -= t
            prev = b
        return res
{{< / highlight >}}
</div>
</div>
