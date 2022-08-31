---
weight: 1152
title: "1152 Analyze User Website Visit Pattern"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_hash_table", "lc_sorting"]
---

You are given two string arrays `username` and `website` and an integer array timestamp. All the given arrays are of the same length and the tuple `[username[i], website[i], timestamp[i]]` indicates that the user `username[i]` visited the website `website[i]` at time `timestamp[i]`.

A **pattern** is a list of three websites (not necessarily distinct).

- For example, `["home", "away", "love"]`, `["leetcode", "love", "leetcode"]`, and `["luffy", "luffy", "luffy"]` are all patterns.

The **score** of a **pattern** is the number of users that visited all the websites in the pattern in the same order they appeared in the pattern.

- For example, if the pattern is `["home", "away", "love"]`, the score is the number of users `x` such that `x` visited "home" then visited `"away"` and visited `"love"` after that.
- Similarly, if the pattern is `["leetcode", "love", "leetcode"`], the score is the number of users `x` such that `x` visited `"leetcode"` then visited `"love"` and visited `"leetcode"` **one more time** after that.
- Also, if the pattern is `["luffy", "luffy", "luffy"]`, the score is the number of users `x` such that `x` visited `"luffy"` three different times at different timestamps.

Return _the **pattern** with the largest **score**_. If there is more than one pattern with the same largest score, return the lexicographically smallest such pattern.

**Example 1:**
```
Input:
username = ["joe","joe","joe","james","james","james","james","mary","mary","mary"],
timestamp = [1,2,3,4,5,6,7,8,9,10],
website = ["home","about","career","home","cart","maps","home","home","about","career"]

Output: ["home","about","career"]
Explanation: The tuples in this example are:
["joe","home",1],["joe","about",2],["joe","career",3],["james","home",4],
["james","cart",5],["james","maps",6],["james","home",7],["mary","home",8],
["mary","about",9], and ["mary","career",10].
The pattern ("home", "about", "career") has score 2 (joe and mary).
The pattern ("home", "cart", "maps") has score 1 (james).
The pattern ("home", "cart", "home") has score 1 (james).
The pattern ("home", "maps", "home") has score 1 (james).
The pattern ("cart", "maps", "home") has score 1 (james).
The pattern ("home", "home", "home") has score 0 (no user visited home 3 times).
```
**Example 2:**
```
Input:
username = ["ua","ua","ua","ub","ub","ub"],
timestamp = [1,2,3,4,5,6],
website = ["a","b","a","a","b","c"]

Output: ["a","b","a"]
```

**Constraints:**
- `3 <= username.length <= 50`
- `1 <= username[i].length <= 10`
- `timestamp.length == username.length`
- <code>1 <= timestamp[i] <= 10<sup>9</sup></code>
- `website.length == username.length`
- `1 <= website[i].length <= 1`0
- `username[i]` and `website[i]` consist of lowercase English letters.
- It is guaranteed that there is at least one user who visited at least three websites.
- All the tuples `[username[i], timestamp[i], website[i]]` are unique.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def mostVisitedPattern(
        self,
        username: List[str],
        timestamp: List[int],
        website: List[str]
    ) -> List[str]:
        records = sorted(
            zip(username, timestamp, website),
            key = lambda x: (x[0],x[1])
        )
        
        visits = {}
        for r in records:
            visits.setdefault(r[0], []).append(r[2])
        
        def select_three(
            lst: List[str],
            selected: List[str],
            res: List[List[str]]
        ) -> None:
            if len(selected) == 3:
                res.append(selected)
                return
            if not lst:
                return
            select_three(lst[1:], selected+[lst[0]], res)
            select_three(lst[1:], selected, res)
        
        pattern_count = {}
        for user in visits:
            patterns = []
            select_three(visits[user], [], patterns)
            for p in set([tuple(p) for p in patterns]):
                pattern_key = tuple(p)
                pattern_count[pattern_key] = pattern_count.get(pattern_key, 0) + 1
        sorted_count = sorted(
            pattern_count.items(),
            key=lambda pair: (-pair[1], pair[0])
        )
        return sorted_count[0][0]

'''
Shorter Version
'''
class Solution:
    def mostVisitedPattern(
        self,
        username: List[str],
        timestamp: List[int],
        website: List[str]
    ) -> List[str]:
        users = defaultdict(list)
        for user, time, site in sorted(
            zip(username, timestamp, website),
            key = lambda x: (x[0],x[1])
        ): 
            users[user].append(site)
        patterns = Counter()
        for user, sites in users.items():
            patterns.update(
                Counter(
                    set(combinations(sites, 3))
                )
            )
        return max(
            sorted(patterns),
            key=patterns.get
        )
{{< / highlight >}}
</div>
</div>
