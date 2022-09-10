---
weight: 735
title: "735 Asteroid Collision"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack"]
---

We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**
```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.
```
**Example 2:**
```
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
```
**Example 3:**
```
Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5.
The 10 and -5 collide resulting in 10.
```

**Constraints:**
- <code>2 <= asteroids.length <= 10<sup>4</sup></code>
- `-1000 <= asteroids[i] <= 1000`
- `asteroids[i] != 0`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []
        for a in asteroids:
            push_new = True
            while stack and a < 0 < stack[-1]:
                if stack[-1] < -a:
                    push_new = True
                    stack.pop()
                    continue
                elif stack[-1] == -a:
                    stack.pop()
                push_new = False
                break
            if push_new:
                stack.append(a)
        return stack
{{< / highlight >}}
</div>
</div>
