---
layout: post
published: true
title: "249. Group Shifted Strings"
categories: interview
tags: medium string 
---

> 문자열의 배열이 주어지면 동일한 이동 시퀀스에 속하는 모든 문자열를 그룹화  
> - 각 문자를 연속 문자로 이동하여 문자열을 이동할 수 있다.

[249. Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings/)

```java
class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        List<List<String>> result = new ArrayList<>();
        
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        
        for (String str : strings) {
            int offset = str.charAt(0) - 'a';
            String key = "";
            
            for (int i = 0; i < str.length(); i++) {
                char c = (char) (str.charAt(i) - offset);
                if (c < 'a') {
                    c += 26;
                }
                key += c;
            }
            
            if (!map.containsKey(key)) {
                List<String> list = new ArrayList<>();
                map.put(key, list);
            }
            
            map.get(key).add(str);
        }
        
        for (String key : map.keySet()) {
            List<String> list = map.get(key);
            Collections.sort(list);
            result.add(list);
        }
        
        return result;
    }
}
```