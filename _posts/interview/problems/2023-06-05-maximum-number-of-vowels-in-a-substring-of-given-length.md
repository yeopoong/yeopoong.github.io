---
layout: post
published: true
title: "1456. Maximum Number of Vowels in a Substring of Given Length"
categories: interview
tags: string
---

> 문자열 s와 정수 k가 주어지면 길이가 k인 s의 하위 문자열에서 최대 모음 문자 수를 반환

[1456. Maximum Number of Vowels in a Substring of Given Length](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)

```java
class Solution {
    
    // 주어진 길이의 하위 문자열에서 최대 모음 수
    // T: O(n)
    public int maxVowels(String s, int k) {
        int ans = 0;
        
        Set<Character> vowels = Set.of('a', 'e', 'i', 'o', 'u');
        
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            if (vowels.contains(s.charAt(i))) {
                ++count; 
            }
            
            // * 이전 윈도우의 마지막 문자가 모음이면 카운트를 감소한다.
            if (i >= k && vowels.contains(s.charAt(i - k))) {
                --count;
            }
            
            ans = Math.max(count, ans);
        }
        
        return ans;
    }
}
```

