---
weight: 418
title: "418 Sentence Screen Fitting"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_string"]
---

Given a `rows x cols` screen and a `sentence` represented as a list of strings, return _the number of times the given sentence can be fitted on the screen_.

The order of words in the sentence must remain unchanged, and a word cannot be split into two lines. A single space must separate two consecutive words in a line.

**Example 1:**
```
Input: sentence = ["hello","world"], rows = 2, cols = 8
Output: 1
Explanation:
hello---
world---
The character '-' signifies an empty space on the screen.
```
**Example 2:**
```
Input: sentence = ["a", "bcd", "e"], rows = 3, cols = 6
Output: 2
Explanation:
a-bcd- 
e-a---
bcd-e-
The character '-' signifies an empty space on the screen.
```
**Example 3:**
```
Input: sentence = ["i","had","apple","pie"], rows = 4, cols = 5
Output: 1
Explanation:
i-had
apple
pie-i
had--
The character '-' signifies an empty space on the screen.
```

**Constraints:**
- `1 <= sentence.length <= 100`
- `1 <= sentence[i].length <= 10`
- `sentence[i]` consists of lowercase English letters.
- <code>1 <= rows, cols <= 2 * 10<sup>4</sup></code>

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def wordsTyping(self, sentence: List[str], rows: int, cols: int) -> int:
        s = ' '.join(sentence) + ' '
        start, L = 0, len(s)
        for i in range(rows):
            start += cols
            if s[start % L] == ' ':
                start += 1
            else:
                while start > 0 and s[(start-1) % L] != ' ':
                    start -= 1
        return start // L
{{< / highlight >}}
</div>
</div>
