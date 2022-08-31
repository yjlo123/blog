---
weight: 1268
title: "1268 Search Suggestions System"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_binary_search", "lc_trie", "lc_string"]
---

You are given an array of strings `products` and a string `searchWord`.

Design a system that suggests at most three product names from `products` after each character of `searchWord` is typed. Suggested products should have common prefix with `searchWord`. If there are more than three products with a common prefix return the three lexicographically minimums products.

Return _a list of lists of the suggested products after each character of `searchWord` is typed._

**Example 1:**
```
Input: products = ["mobile","mouse","moneypot","monitor","mousepad"], searchWord = "mouse"
Output: [
["mobile","moneypot","monitor"],
["mobile","moneypot","monitor"],
["mouse","mousepad"],
["mouse","mousepad"],
["mouse","mousepad"]
]
Explanation: products sorted lexicographically = ["mobile","moneypot","monitor","mouse","mousepad"]
After typing m and mo all products match and we show user ["mobile","moneypot","monitor"]
After typing mou, mous and mouse the system suggests ["mouse","mousepad"]
```
**Example 2:**
```
Input: products = ["havana"], searchWord = "havana"
Output: [["havana"],["havana"],["havana"],["havana"],["havana"],["havana"]]
Example 3:

Input: products = ["bags","baggage","banner","box","cloths"], searchWord = "bags"
Output: [["baggage","bags","banner"],["baggage","bags","banner"],["baggage","bags"],["bags"]]
```

**Constraints:**
- `1 <= products.length <= 1000`
- `1 <= products[i].length <= 3000`
- <code>1 <= sum(products[i].length) <= 2 * 10<sup>4</sup></code>
- All the strings of `products` are **unique**.
- `products[i]` consists of lowercase English letters.
- `1 <= searchWord.length <= 1000`
- `searchWord` consists of lowercase English letters.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from bisect import bisect_left

class Solution:
    def suggestedProducts(
        self,
        products: List[str],
        searchWord: str
    ) -> List[List[str]]:
        sorted_products = sorted(products)
        res = []
        i = 0
        pre = ''
        
        for c in searchWord:
            pre += c
            i = bisect_left(sorted_products, pre, i)
            res.append([
                w for w in sorted_products[i:i+3] if w.startswith(pre)
            ])
        return res
{{< / highlight >}}
</div>
</div>
