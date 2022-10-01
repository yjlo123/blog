---
weight: 155
title: "155 Min Stack"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_stack", "lc_ood"]
---

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
-` void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**
```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

**Constraints:**
- <code>-2<sup>31</sup> <= val <= 2<sup>31</sup> - 1</code>
- Methods `pop`, `top` and `getMin` operations will always be called on non-empty stacks.
- At most <code>3 * 10<sup>4</sup></code> calls will be made to `push`, `pop`, `top`, and `getMin`.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class MinStack:

    def __init__(self):
        self.data = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.data.append(val)
        if not self.min_stack or val < self.min_stack[-1][0]:
            self.min_stack.append([val, 1])
        elif val == self.min_stack[-1][0]:
            self.min_stack[-1][1] += 1
            

    def pop(self) -> None:
        if self.min_stack[-1][0] == self.data[-1]:
            self.min_stack[-1][1] -= 1

        if self.min_stack[-1][1] == 0:
            self.min_stack.pop()
            
        self.data.pop()

    def top(self) -> int:
        return self.data[-1]

    def getMin(self) -> int:
        return self.min_stack[-1][0]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
{{< / highlight >}}
</div>
</div>
