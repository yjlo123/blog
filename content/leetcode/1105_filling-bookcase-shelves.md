---
weight: 1105
title: "1105 Filling Bookcase Shelves"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_dp"]
---

You are given an array `books` where <code>books[i] = [thickness<sub>i</sub>, height<sub>i</sub>]</code> indicates the thickness and height of the <code>i<sup>th</sup></code> book. You are also given an integer `shelfWidth`.

We want to place these books in order onto bookcase shelves that have a total width `shelfWidth`.

We choose some of the books to place on this shelf such that the sum of their thickness is less than or equal to `shelfWidth`, then build another level of the shelf of the bookcase so that the total height of the bookcase has increased by the maximum height of the books we just put down. We repeat this process until there are no more books to place.

Note that at each step of the above process, the order of the books we place is the **same order** as the given sequence of books.

- For example, if we have an ordered list of `5` books, we might place the first and second book onto the first shelf, the third book on the second shelf, and the fourth and fifth book on the last shelf.

Return _the minimum possible height that the total bookshelf can be after placing shelves in this manner_.


**Example 1:**
```
1___  <- 1st shelf
2233
2233
2233  <- 2nd shelf
___7
4567  <- 3rd shelf

Input: books = [[1,1],[2,3],[2,3],[1,1],[1,1],[1,1],[1,2]], shelf_width = 4
Output: 6
Explanation:
The sum of the heights of the 3 shelves is 1 + 3 + 2 = 6.
Notice that book number 2 does not have to be on the first shelf.
```
**Example 2:**
```
Input: books = [[1,3],[2,4],[3,2]], shelfWidth = 6
Output: 4
```

**Constraints:**
- `1 <= books.length <= 1000`
- <code>1 <= thickness<sub>i</sub> <= shelfWidth <= 1000</code>
- <code>1 <= height<sub>i</sub> <= 1000</code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def minHeightShelves(self, books: List[List[int]], shelfWidth: int) -> int:
        n = len(books)
        # dp[i] := min height if i-th books is the last book
        #          on its current level
        dp = [0] + [math.inf] * n

        for i in range(1, n + 1):
            # max height of the current level
            max_height = 0
            remaining = shelfWidth
            
            # try all possible previous book (within shelfWidth)
            # [i down to j] at the same level with the current book (i)
            for j in range(i, 0, -1):
                # including the current book (i)
                w, h = books[j - 1]
                max_height = max(max_height, h)
                remaining -= w
                
                if remaining < 0:
                    break
                
                dp[i] = min(dp[i], dp[j - 1] + max_height)
        
        return dp[n]
{{< / highlight >}}
</div>
</div>
