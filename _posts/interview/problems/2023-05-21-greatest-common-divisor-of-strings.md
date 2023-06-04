---
layout: post
published: true
title: "1071. Greatest Common Divisor of Strings"
categories: interview
tags: string math
---

> 두 개의 문자열 str1과 str2가 주어지면 x가 str1과 str2를 모두 나누는 가장 큰 문자열 x를 반환

- [1071. Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings/)

```java
class Solution {
    
    // 문자열의 최대 공약수
    // T: O(m + n)
    public String gcdOfStrings(String str1, String str2) {
        // Check if they have non-zero GCD string.
        if (!(str1 + str2).equals(str2 + str1)) {
            return "";
        }
        
        // 문자열 길이로 최대 공약수를 구한다.
        int gcdLength = getGCDLength(str1.length(), str2.length());
        
        // 최대 공약수로 문자열을 서브 스트링해서 리턴한다.
        return str1.substring(0, gcdLength);
    }
    
    public int getGCDLength(int x, int y) {
        if (y == 0) {
            return x;
        } else {
            return getGCDLength(y, x % y);
        }    
    }
    
}
```