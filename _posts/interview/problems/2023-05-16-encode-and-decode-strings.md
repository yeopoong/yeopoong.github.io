---
layout: post
published: true
title: "271. Encode and Decode Strings"
categories: interview
tags: problems string design
---

> 문자열 목록을 문자열로 인코딩하는 알고리즘을 설계  
> 그런 다음 인코딩된 문자열은 네트워크를 통해 전송되고 원래 문자열 목록으로 다시 디코딩

- [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder encodedString = new StringBuilder();
        
        for (String str : strs) {
            encodedString.append(str.length()).append("#").append(str);
        }
        
        return encodedString.toString();
    }

    // Decodes a single string to a list of strings.
    // 5#Hello5#World
    // T: O(n)
    public List<String> decode(String s) {
        List<String> list = new ArrayList<>();
        
        int i = 0;
        while (i < s.length()) {
            int j = i;
            // 문자길이 마지막 위치 
            while (s.charAt(j) != '#') j++;

            // 문자길이 파싱
            int length = Integer.valueOf(s.substring(i, j));
            
            // 문자종료 인덱스
            i = j + 1 + length;
            
            // 문자열 = 문자시작위치 ~ 문자종료위치
            list.add(s.substring(j + 1, i));
        }
        
        return list;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```