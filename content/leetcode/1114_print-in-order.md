---
weight: 1114
title: "1114 Print in Order"
date: 2021-03-22T00:00:00+08:00
draft: false
tags: ["leetcode", "lc_easy", "lc_concurrency", "lc_ood"]
---

Suppose we have a class:
```
public class Foo {
  public void first() { print("first"); }
  public void second() { print("second"); }
  public void third() { print("third"); }
}
```
The same instance of `Foo` will be passed to three different threads. Thread A will call `first()`, thread B will call `second()`, and thread C will call `third()`. Design a mechanism and modify the program to ensure that `second()` is executed after `first()`, and `third()` is executed after `second()`.

**Example 1:**
```
Input: [1,2,3]
Output: "firstsecondthird"
Explanation: There are three threads being fired asynchronously.
The input [1,2,3] means thread A calls first(), thread B calls second(), and thread C calls third().
"firstsecondthird" is the correct output.
```
**Example 2:**
```
Input: [1,3,2]
Output: "firstsecondthird"
Explanation: The input [1,3,2] means thread A calls first(), thread B calls third(),
and thread C calls second(). "firstsecondthird" is the correct output.
```

**Note:**
We do not know how the threads will be scheduled in the operating system, even though the numbers in the input seems to imply the ordering. The input format you see is mainly to ensure our tests' comprehensiveness.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from threading import Event

class Foo:
    def __init__(self):
        self.done = (Event(), Event())


    def first(self, printFirst: 'Callable[[], None]') -> None:
        
        # printFirst() outputs "first". Do not change or remove this line.
        printFirst()
        self.done[0].set()


    def second(self, printSecond: 'Callable[[], None]') -> None:
        
        self.done[0].wait()
        # printSecond() outputs "second". Do not change or remove this line.
        printSecond()
        self.done[1].set()


    def third(self, printThird: 'Callable[[], None]') -> None:
        
        self.done[1].wait()
        # printThird() outputs "third". Do not change or remove this line.
        printThird()
        
{{< / highlight >}}
</div>
</div>
