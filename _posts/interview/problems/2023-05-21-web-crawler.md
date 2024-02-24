---
layout: post
published: true
title: "1236. Web Crawler"
categories: interview
tags: medium string bfs
---

> URL startUrl 및 인터페이스 HtmlParser가 있는 경우 웹 크롤러를 구현하여 startUrl과 동일한 호스트 이름에 있는 모든 링크를 크롤링

[1236. Web Crawler](https://leetcode.com/problems/web-crawler/)

![](https://assets.leetcode.com/uploads/2019/08/13/urlhostname.png)

BFS
```java
/**
 * // This is the HtmlParser's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface HtmlParser {
 *     public List<String> getUrls(String url) {}
 * }
 */

class Solution {
    
    public List<String> crawl(String startUrl, HtmlParser htmlParser) {
        Set<String> set = new HashSet<>();
        
        Queue<String> queue = new LinkedList<>();
        String hostname = getHostname(startUrl);
        
        queue.offer(startUrl);
        set.add(startUrl);
        
        while (!queue.isEmpty()) {
            String currentUrl = queue.poll();
            for (String url : htmlParser.getUrls(currentUrl)) {
                if (url.contains(hostname) && !set.contains(url)) {
                    queue.offer(url);
                    set.add(url);
                }
            }
        }
        
        return new ArrayList<String>(set);
    }
    
    private String getHostname(String Url) {
        String[] ss = Url.split("/");
        return ss[2];
    }
}
```

DFS
```java
/**
 * // This is the HtmlParser's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface HtmlParser {
 *     public List<String> getUrls(String url) {}
 * }
 */

class Solution {

    private String startHostname;
    private HashSet<String> visited = new HashSet<String>();
    
    // T: O(ml), m: the number of edges, l: the maximum length of a URL
    public List<String> crawl(String startUrl, HtmlParser htmlParser) {
        startHostname = getHostname(startUrl);
        dfs(startUrl, htmlParser);
        return new ArrayList<>(visited);
    }

    private void dfs(String url, HtmlParser htmlParser) {
        visited.add(url);
        for (String nextUrl : htmlParser.getUrls(url)) {
            if (getHostname(nextUrl).equals(startHostname) && !visited.contains(nextUrl)) {
                dfs(nextUrl, htmlParser);
            }
        }
    }
    
    private String getHostname(String url) {
        String[] ss = url.split("/");
        return ss[2];
    }
}
```