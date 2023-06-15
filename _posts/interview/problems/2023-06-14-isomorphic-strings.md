---
layout: post
published: true
title: "205. Isomorphic Strings"
categories: interview
tags: easy hashmap
---

> 두 문자열 s와 t가 주어지면 동형인지 확인  
> : 두 개의 문자열 s와 t는 s의 문자를 t로 대체할 수 있는 경우 동형

[205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

```java
class Solution {
    // 동형 문자열
    public boolean isIsomorphic(String s, String t) {
        
        //맵에 인덱스 값을 저장한다.
        Map<Object, Integer> index1 = new HashMap();
        Map<Object, Integer> index2 = new HashMap();
        
        for (Integer i = 0; i < s.length(); ++i) {
            //패턴의 인덱스값이 같지 않으면 다른 패턴이다.
            //return value is the previous value associated with key, or null
            if (index1.put(s.charAt(i), i) != index2.put(t.charAt(i), i)) {
                return false;
            }
        }
            
        return true;   
    }
}
```
