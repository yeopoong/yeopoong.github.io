---
layout: post
published: true
title: "49. Group Anagrams"
categories: interview
tags: problems hashmap
---

> 문자열의 배열이 주어지면 아나그램을 함께 그룹화

- [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)

```java
class Solution {
    // 아나그램 그룹핑
    // T: O(nklogk), n is the length of strs, k is the maximum length of string in strs.
    // S: O(nm)
    public List<List<String>> groupAnagrams(String[] strs) {
        // 그룹핑 하기위해서 맵자료 구조를 사용
        Map<String, List<String>> map = new HashMap<>();
        
        for (String s : strs) {
            // 아나그램을 그룹핑 하기위해서 정렬된 문자열을 키로 사용
            char[] ca = s.toCharArray();
            Arrays.sort(ca);
            
            String key = String.valueOf(ca);
            List list = map.get(key);
            // 키가 존재하지 않으면 리스트 추가
            if (list == null) {
                list = new ArrayList<>();
                map.put(key, list);
            }
            
            // 문자열을 키 그룹에 추가
            list.add(s);
        }
        
        return new ArrayList<>(map.values());
    }
}
```