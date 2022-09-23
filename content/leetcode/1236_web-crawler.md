---
weight: 1236
title: "1236 Web Crawler"
date: 2022-09-01T00:00:00-04:00
draft: false
tags: ["leetcode", "lc_medium", "lc_interactive", "lc_bfs"]
---

Given a url `startUrl` and an interface `HtmlParser`, implement a web crawler to crawl all links that are under the **same hostname** as `startUrl`. 

Return all urls obtained by your web crawler in **any** order.

Your crawler should:
- Start from the page: `startUrl`
- Call `HtmlParser.getUrls(url)` to get all urls from a webpage of given url.
- Do not crawl the same link twice.
- Explore only the links that are under the **same hostname** as `startUrl`.
```
https://example.org:8888/foo/bar#bang
        -hostname--
        ------host------
```
As shown in the example url above, the hostname is `example.org`. For simplicity sake, you may assume all urls use **http protocol** without any **port** specified. For example, the urls `http://leetcode.com/problems` and `http://leetcode.com/contest` are under the same hostname, while urls `http://example.org/test` and `http://example.com/abc` are not under the same hostname.

The `HtmlParser` interface is defined as such: 
```
interface HtmlParser {
  // Return a list of all urls from a webpage of given url.
  public List<String> getUrls(String url);
}
```
Below are two examples explaining the functionality of the problem, for custom testing purposes you'll have three variables `urls`, `edges` and `startUrl`. Notice that you will only have access to `startUrl` in your code, while `urls` and `edges` are not directly accessible to you in code.

**Example 1:**
<img src="https://assets.leetcode.com/uploads/2019/10/23/sample_2_1497.png" style="width: 100%;"/>
```
Input:
urls = [
  "http://news.yahoo.com",
  "http://news.yahoo.com/news",
  "http://news.yahoo.com/news/topics/",
  "http://news.google.com",
  "http://news.yahoo.com/us"
]
edges = [[2,0],[2,1],[3,2],[3,1],[0,4]]
startUrl = "http://news.yahoo.com/news/topics/"
Output: [
  "http://news.yahoo.com",
  "http://news.yahoo.com/news",
  "http://news.yahoo.com/news/topics/",
  "http://news.yahoo.com/us"
]
```
**Example 2:**
<img src="https://assets.leetcode.com/uploads/2019/10/23/sample_3_1497.png" style="width: 100%;"/>
```
Input: 
urls = [
  "http://news.yahoo.com",
  "http://news.yahoo.com/news",
  "http://news.yahoo.com/news/topics/",
  "http://news.google.com"
]
edges = [[0,2],[2,1],[3,2],[3,1],[3,0]]
startUrl = "http://news.google.com"
Output: ["http://news.google.com"]
Explanation: The startUrl links to all other pages that do not share the same hostname.
```

**Constraints:**
- `1 <= urls.length <= 1000`
- `1 <= urls[i].length <= 300`
- `startUrl` is one of the `urls`.
- Hostname label must be from 1 to 63 characters long, including the dots, may contain only the ASCII letters from 'a' to 'z', digits  from '0' to '9' and the hyphen-minus character ('-').
- The hostname may not start or end with the hyphen-minus character ('-'). 
- See: [https://en.wikipedia.org/wiki/Hostname#Restrictions_on_valid_hostnames](https://en.wikipedia.org/wiki/Hostname#Restrictions_on_valid_hostnames)
- You may assume there're no duplicates in url library.

<div class="tabs"></div>
<div class="tab-content">
<div id="python" class="lang">
{{< highlight python "linenos=table" >}}
# """
# This is HtmlParser's API interface.
# You should not implement it, or speculate about its implementation
# """
#class HtmlParser(object):
#    def getUrls(self, url):
#        """
#        :type url: str
#        :rtype List[str]
#        """

class Solution:
    @staticmethod
    def get_host(url: str) -> str:
        return url.split('//')[1].split('/')[0]
    
    def crawl(self, startUrl: str, htmlParser: 'HtmlParser') -> List[str]:
        host = self.get_host(startUrl)
        seen = set([startUrl])
        q = deque([startUrl])
        while q:
            url = q.popleft()
            children = htmlParser.getUrls(url)
            for u in children:
                if self.get_host(u) != host or u in seen:
                    continue
                q.append(u)
                seen.add(u)
        return list(seen)
{{< / highlight >}}
</div>
</div>
