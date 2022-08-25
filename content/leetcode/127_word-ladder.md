---
weight: 127
title: "127 Word Ladder"
date: 2022-08-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_string", "lc_bfs", "lc_hash_table"]
---

A **transformation sequence** from word `beginWord` to word endWord using a dictionary `wordList` is a sequence of words <code>beginWord -> s<sub>1</sub> -> s<sub>2</sub> -> ... -> s<sub>k</sub></code> such that:
- Every adjacent pair of words differs by a single letter.
- Every <code>s<sub>i</sub></code> for `1 <= i <= k` is in wordList. Note that `beginWord` does not need to be in wordList.
- <code>s<sub>k</sub> == endWord</code>
Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _the **number of words** in the **shortest transformation sequence** from `beginWord` to `endWord`, or `0` if no such sequence exists._

**Example 1:**
```
Input: beginWord = "hit", endWord = "cog",
       wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is
"hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```
**Example 2:**
```
Input: beginWord = "hit", endWord = "cog",
       wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList,
therefore there is no valid transformation sequence.
```

**Constraints:**
- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
- `beginWord != endWord`
- All the words in `wordList` are **unique**.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
from collections import defaultdict, deque

class Solution:
    def __init__(self):
        self.len = 0
        self.all_d = defaultdict(list)
    
    def get_inter_word(self, word: str, i: int) -> str:
        return word[:i] + "*" + word[i+1:]
    
    def visit_word(self, q: deque, visited: dict, others_visited:dict) -> Optional[int]:
        for _ in range(len(q)):
            current_word = q.popleft()
            for i in range(self.len):
                for word in self.all_d[self.get_inter_word(current_word, i)]:
                    if word in others_visited:
                        return visited[current_word] + others_visited[word]
                    if word not in visited:
                        visited[word] = visited[current_word] + 1
                        q.append(word)
        return None
    
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if (not beginWord
            or not endWord
            or not wordList
            or endWord not in wordList):
            return 0
        
        self.len = len(beginWord)
        
        for word in wordList:
            for i in range(self.len):
                self.all_d[self.get_inter_word(word, i)].append(word)
            
        q_begin = deque([beginWord])
        q_end = deque([endWord])

        visited_begin = {beginWord: 1}
        visited_end = {endWord: 1}
        ans = None

        while q_begin and q_end:
            if len(q_begin) <= len(q_end):
                ans = self.visit_word(q_begin, visited_begin, visited_end)
            else:
                ans = self.visit_word(q_end, visited_end, visited_begin)
            if ans:
                return ans
        return 0
{{< / highlight >}}
</div>
</div>
