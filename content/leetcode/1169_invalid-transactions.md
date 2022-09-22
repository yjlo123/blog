---
weight: 1169
title: "1169 Invalid Transactions"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_sorting", "lc_hash_table"]
---

A transaction is possibly invalid if:
- the amount exceeds `$1000`, or;
- if it occurs within (and including) `60` minutes of another transaction with the **same name** in a **different city**.

You are given an array of strings `transaction` where `transactions[i]` consists of comma-separated values representing the name, time (in minutes), amount, and city of the transaction.

Return a list of `transactions` that are possibly invalid. You may return the answer in any order.

**Example 1:**
```
Input: transactions = ["alice,20,800,mtv","alice,50,100,beijing"]
Output: ["alice,20,800,mtv","alice,50,100,beijing"]
Explanation: The first transaction is invalid because the second transaction
occurs within a difference of 60 minutes, have the same name and is in a
different city. Similarly the second one is invalid too.
```
**Example 2:**
```
Input: transactions = ["alice,20,800,mtv","alice,50,1200,mtv"]
Output: ["alice,50,1200,mtv"]
```
**Example 3:**
```
Input: transactions = ["alice,20,800,mtv","bob,50,1200,mtv"]
Output: ["bob,50,1200,mtv"]
```

**Constraints:**
- `transactions.length <= 1000`
- Each `transactions[i]` takes the form `"{name},{time},{amount},{city}"`
- Each `{name}` and `{city}` consist of lowercase English letters, and have lengths between `1` and `10`.
- Each `{time}` consist of digits, and represent an integer between `0` and `1000`.
- Each `{amount}` consist of digits, and represent an integer between `0` and `2000`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def invalidTransactions(self, transactions: List[str]) -> List[str]:
        # Group by name
        d = {}
        for t in transactions:
            name, time, amount, city = t.split(',')
            d.setdefault(name, []).append((int(time), int(amount), city))

        # Sort by time for each name
        for n in d:
            d[n].sort(key=lambda t: t[0])

        res = []
        for name, txns in d.items():
            invalid = set()
            for i, txn in enumerate(txns):
                if txn[1] > 1000:
                    invalid.add((i, txn))
                if i == 0:
                    continue
                j = i - 1
                while j >= 0:
                    prev = txns[j]
                    if txn[0] - prev[0] > 60:
                        break
                    if txn[2] != prev[2]:
                        invalid.add((i, txn))
                        invalid.add((j, prev))
                    j -= 1
            for i in invalid:
                res.append('{},{},{},{}'.format(name, *i[1]))
        return res
{{< / highlight >}}
</div>
</div>
