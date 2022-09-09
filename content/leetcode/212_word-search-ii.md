---
weight: 212
title: "212 Word Search II"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_hard", "lc_trie", "lc_matrix"]
---

Given an `m x n` board of characters and a list of strings words, return _all words on the board_.

Each word must be constructed from letters of sequentially **adjacent cells**, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**
```
Input: board = [
    ["o","a","a","n"],
    ["e","t","a","e"],
    ["i","h","k","r"],
    ["i","f","l","v"]
], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```
**Example 2:**
```
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
```

**Constraints:**
- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 12`
- `board[i][j]` is a lowercase English letter.
- <code>1 <= words.length <= 3 * 10<sup>4</sup></code>
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- All the strings of `words` are unique.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
class Solution:
    def findWords(
        self,
        board: List[List[str]],
        words: List[str]
    ) -> List[str]:
        def prune_shitty_trie(root, word):
            prune_candidate = (root, word[0])
            current = root

            i = 0
            while i < len(word):
                char = word[i]
                if current[char]["is_word"] or len(current[char]) > 2:
                    # can't prune anything above and including current[char]
                    if i + 1 >= len(word):
                        return
                    prune_candidate = (current[char], word[i + 1])

                current = current[char]
                i += 1

            if len(current) == 1:
                del prune_candidate[0][prune_candidate[1]]

        def dfs(r, c, node, accumulated):
            if r < 0 or r >= m or c < 0 or c >= n:
                return

            if board[r][c] not in node:
                return

            char = board[r][c]
            board[r][c] = "#"
            accumulated += char
            node = node[char]

            if node["is_word"]:
                res.append(accumulated)
                node["is_word"] = False
                prune_shitty_trie(root, accumulated)

            # 4 directions
            for (dr, dc) in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                dfs(r + dr, c + dc, node, accumulated)

            board[r][c] = char

        m, n = len(board), len(board[0])
        
        # Build trie
        root = {"is_word": False}
        for word in words:
            current = root
            for char in word:
                current = current.setdefault(char, {"is_word": False})
            current["is_word"] = True

        res = []
        for r in range(m):
            for c in range(n):
                dfs(r, c, root, '')

        return res
{{< / highlight >}}
</div>
</div>
