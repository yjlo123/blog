---
weight: 68
title: "68 Text Justification"
date: 2023-01-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_string"]
---

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**
- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
- The input array words contains at least one word.

**Example 1:**
```
Input:
 words = ["This", "is", "an", "example", "of", "text", "justification."],
 maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```
**Example 2:**
```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be",
because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
```
**Example 3:**
```
Input:
 words = [
    "Science","is","what","we","understand","well","enough","to",
    "explain","to","a","computer.","Art","is","everything","else","we","do"],
 maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

**Constraints:**
- `1 <= words.length <= 300`
- `1 <= words[i].length <= 20`
- `words[i]` consists of only English letters and symbols.
- `1 <= maxWidth <= 100`
- `words[i].length <= maxWidth`

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        line = [words[0]]
        content_len = line_len = len(words[0])
        res = []

        for i in range(1, len(words)):
            w = words[i]
            if line_len + len(w) + 1 <= maxWidth:
                # add word to the current line
                line.append(w)
                line_len += len(w) + 1
                content_len += len(w)
            else:
                if len(line) == 1:
                    # one-word line
                    res.append(line[0] + ' ' * (maxWidth - len(line[0])))
                else:
                    space_len = maxWidth - content_len
                    space_count = len(line) - 1
                    extra_space_count = space_len % space_count
                    space_base = ' ' * (space_len // space_count)
                    line_with_space = [line[0]]
                    for i in range(1, len(line)):
                        line_with_space.append(space_base if i > extra_space_count else space_base+' ')
                        line_with_space.append(line[i])
                    res.append(''.join(line_with_space))
                # new line
                line = [w]
                content_len = line_len = len(w)

        if line:
            # last line
            content_str = ' '.join(line)
            res.append(content_str + ' ' * (maxWidth - len(content_str)))

        return res
{{< / highlight >}}
</div>
</div>
