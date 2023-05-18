---
layout: post
published: true
title: "140. Word Break II"
categories: interview
tags: problems backtracking matrix
---

> 문자열 s와 문자열 wordDict의 사전이 주어지면 s에 공백을 추가하여 각 단어가 유효한 사전 단어인 문장을 구성

- [140. Word Break II](https://leetcode.com/problems/word-break-ii/)

```java
class Solution {
    
    HashMap<String, List<String>> map = new HashMap<>();
    
    public List<String> wordBreak(String s, List<String> wordDict) {
        return dfs(s, wordDict);
    }       

    // dfs function returns an array including all substrings derived from s.
    private List<String> dfs(String s, List<String> wordDict) {
        if (map.containsKey(s)) {
            return map.get(s);
        }

        List<String> res = new LinkedList<String>();     
        if (s.length() == 0) {
            res.add("");
            return res;
        }               
        
        for (String word : wordDict) {
            if (s.startsWith(word)) {
                List<String>sublist = dfs(s.substring(word.length()), wordDict);
                for (String sub : sublist) 
                    res.add(word + (sub.isEmpty() ? "" : " ") + sub);               
            }
        }       
        
        map.put(s, res);
        
        return res;
    }
}
```