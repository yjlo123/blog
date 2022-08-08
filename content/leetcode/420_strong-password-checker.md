---
weight: 420
title: "420 Strong Password Checker"
date: 2022-08-08T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard"]
---

A password is considered strong if the below conditions are all met:
- It has at least `6` characters and at most `20` characters.
- It contains at least **one lowercase** letter, at least **one uppercase** letter, and at least **one digit**.
- It does not contain three repeating characters in a row (i.e., `"...aaa..."` is weak, but `"...aa...a..."` is strong, assuming other conditions are met).

Given a string `password`, return the minimum number of steps required to make `password` strong. if `password` is already strong, return `0`.

In one step, you can:
- Insert one character to password,
- Delete one character from password, or
- Replace one character of password with another character.

**Example 1:**
```
Input: password = "a"
Output: 5
```

**Example 2:**
```
Input: password = "aA1"
Output: 3
```

**Example 3:**
```
Input: password = "1337C0d3"
Output: 0
```

**Constraints:**

- `1 <= password.length <= 50`
- `password` consists of letters, digits, dot `'.'` or exclamation mark `'!'`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    type_sets = [
        set('abcdefghijklmnopqrstuvwxyz'),
        set('ABCDEFGHIJKLMNOPQRSTUFVWXYZ'),
        set('0123456789'),
    ]
    
    def strongPasswordChecker(self, password: str) -> int:
        chars = set(password)

        # Check rule 1
        num_req_inserts = max(0, 6 - len(password))
        num_req_deletes = max(0, len(password) - 20)

        # Check rule 2
        num_req_types = 0
        for t in self.type_sets:
            num_req_types += 0 if (chars & t) else 1

        # Check rule 3
        groups = [len(list(grp)) for _, grp in itertools.groupby(password)]
        for _ in range(num_req_deletes):
            # Apply best delete
            idx, _ = min(
                enumerate(groups),
                # Ignore groups of length < 3
                # 5 - it[1] > 2 when it[1] < 3
                key=lambda it: it[1] % 3 if it[1] >= 3 else 5,
            )
            groups[idx] -= 1

        num_req_group_replaces = sum(
            group // 3
            for group in groups
        )

        return (
            num_req_deletes
            + max(
                num_req_types,
                num_req_group_replaces,
                num_req_inserts,
                )
            )
{{< / highlight >}}
</div>
</div>
