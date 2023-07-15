---
layout: post
published: true
title: "187. Repeated DNA Sequences"
categories: interview
tags: medium string sliding-window hashmap
---

> 두 번 이상 발생하는 모든 10자 길이의 시퀀스(하위 문자열)를 반환

[187. Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/)

```java
class Solution {
    // 두 번 이상 발생하는 모든 10자 길이의 시퀀스(하위 문자열)를 반환
    // O(n)
    public List<String> findRepeatedDnaSequences(String s) {
        Set<String> repeated = new HashSet<>();
        
        // 중복체크
        Set<String> seen = new HashSet<>();
        
        for (int i = 0; i + 9 < s.length(); i++) {
            // 10자 길이의 시퀀스(하위 문자열)
            String ten = s.substring(i, i + 10);
            
            // 중복이면(두번 이상 발생) 결과집합에 저장
            // true if this set did not already contain the specified element
            if (!seen.add(ten) && !repeated.contains(ten)) {
                // Adds the specified element to this set if it is not already present.
                repeated.add(ten);
            }
        }
        
        return new ArrayList(repeated);
    }
}
```