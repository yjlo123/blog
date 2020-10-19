---
weight: 412
title: "412 Fizz Buzz"
date: 2020-09-24T00:00:00+08:00
draft: false
tags: ["leetcode"]
---

Write a program that outputs the string representation of numbers from 1 to _n_.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

**Example:**
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
<div class="tabs">
  <div class="tab-btn tab-btn-active" onclick="showLang(event, 'golang')">Golang</div>
  <div class="tab-btn" onclick="showLang(event, 'runtime')">Runtime</div>
</div>
<div class="tab-content">
<div id="golang" class="lang">
{{< highlight go "linenos=table" >}}
func fizzBuzz(n int) []string {
    var result []string
    for i := 1; i <= n; i++ {
        if i%3 == 0 && i%5 == 0 {
            result = append(result, "FizzBuzz")
        } else if i%3 == 0 {
            result = append(result, "Fizz")
        } else if i%5 == 0 {
            result = append(result, "Buzz")
        } else {
            result = append(result, strconv.Itoa(i))
        }
    }
    return result
}
{{< / highlight >}}
</div>
<div id="runtime" class="lang" style="display:none">
    <div class="code-link">
        <a href="https://runtime.siwei.dev/?src=leetcode412" target="_blank">https://runtime.siwei.dev/?src=leetcode412</a>
    </div>
</div>
</div>
