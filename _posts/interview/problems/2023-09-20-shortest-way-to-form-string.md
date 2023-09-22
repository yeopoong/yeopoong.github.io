---
layout: post
published: true
title: "1055. Shortest Way to Form String"
categories: interview
tags: medium two-pointers
---

> 두 개의 문자열 source와 target이 주어지면 연결이 target과 같아지도록 source의 하위 시퀀스의 최소 수를 반환

[1055. Shortest Way to Form String](https://leetcode.com/problems/shortest-way-to-form-string/)

```java
class Solution {
    public int shortestWay(String source, String target) {
        int res = 1;
        
        char[] cs = source.toCharArray(), ts = target.toCharArray();
        boolean[] map = new boolean[26];
        
        for (int i = 0; i < cs.length; i++) {
            map[cs[i] - 'a'] = true;
        } 
        
        int j = 0;
        
        for (int i = 0; i < ts.length; i++,j++) {
            if (!map[ts[i] - 'a']) {
                return -1;
            }
            
            while (j < cs.length && cs[j] != ts[i]) {
                j++;
            }
            
            if (j == cs.length) {
                j = -1;
                res++;
                i--;
            }
        }
        
        return res;
    }
}
```