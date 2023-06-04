---
layout: post
published: true
title: "443. String Compression"
categories: interview
tags: string two-pointers
---

> 문자 배열이 주어지면 다음 알고리즘을 사용하여 압축  
> - 그룹의 길이가 1이면 문자를 s에 추가  
> - 그렇지 않으면 문자 뒤에 그룹 길이를 추가

- [443. String Compression](https://leetcode.com/problems/string-compression/)

```java
class Solution {
    
    // 문자 배열이 주어지면 다음 알고리즘을 사용하여 압축 
    public int compress(char[] chars) {
        int indexAns = 0, index = 0;
        
        while (index < chars.length) {
            char currentChar = chars[index];
            int count = 0;
            
            // 다음 문자가 같은 문자이면 포인터와 개수 증가시킨다.
            while (index < chars.length && chars[index] == currentChar) {
                index++;
                count++;
            }
            
            // 현재 문자 저장
            chars[indexAns++] = currentChar;
            
            // 두자리 숫자이면 개별 문자로 저장
            if (count != 1) {
                for (char c : Integer.toString(count).toCharArray()) {
                    chars[indexAns++] = c;
                }
            }
        }
        
        return indexAns;
    }
}
```