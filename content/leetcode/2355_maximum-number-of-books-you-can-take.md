---
weight: 2355
title: "2355 Maximum Number of Books You Can Take"
date: 2023-02-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_dp", "lc_stack"]
---

You are given a **0-indexed** integer array `books` of length `n` where `books[i]` denotes the number of books on the <code>i<sup>th</sup></code> shelf of a bookshelf.

You are going to take books from a contiguous section of the bookshelf spanning from `l` to `r` where `0 <= l <= r < n`. For each index `i` in the range `l <= i < r`, you must take **strictly fewer** books from shelf `i` than shelf `i + 1`.

Return *the **maximum** number of books you can take from the bookshelf*.


**Example 1:**
```
Input: books = [8,5,2,7,9]
Output: 19
Explanation:
- Take 1 book from shelf 1.
- Take 2 books from shelf 2.
- Take 7 books from shelf 3.
- Take 9 books from shelf 4.
You have taken 19 books, so return 19.
It can be proven that 19 is the maximum number of books you can take.
```
**Example 2:**
```
Input: books = [7,0,3,4,5]
Output: 12
Explanation:
- Take 3 books from shelf 2.
- Take 4 books from shelf 3.
- Take 5 books from shelf 4.
You have taken 12 books so return 12.
It can be proven that 12 is the maximum number of books you can take.
```
**Example 3:**
```
Input: books = [8,2,3,7,3,4,0,1,4,3]
Output: 13
Explanation:
- Take 1 book from shelf 0.
- Take 2 books from shelf 1.
- Take 3 books from shelf 2.
- Take 7 books from shelf 3.
You have taken 13 books so return 13.
It can be proven that 13 is the maximum number of books you can take.
```

**Constraints:**
- <code>1 <= books.length <= 10<sup>5</sup></code>
- <code>0 <= books[i] <= 10<sup>5</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def maximumBooks(self, books: List[int]) -> int:
        res = 0
        stack = []
        for i in range(len(books)):
            while (
                stack and
                books[stack[-1][0]] >= books[i] - (i - stack[-1][0])
            ):
                # keep popping from the stack while b[x] ≥ b[i] - (i - x)
                # since if its true, x will never be an index j
                # as index i will run out of items first.
                stack.pop()
            j, j_res = stack[-1] if stack else [-1, 0]
            h = min(i - j, books[i])
            l1, l2 = books[i], books[i] - h + 1
            cur = j_res + (l1 + l2) * h // 2
            stack.append([i, cur])
            res = max(res, cur)
        return res
{{< / highlight >}}
</div>
</div>
