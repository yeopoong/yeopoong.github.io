---
layout: post
published: true
title: "392. Is Subsequence"
categories: interview
tags: problems string two-pointers
---

> 두 문자열 s와 t가 주어지면 s가 t의 하위 시퀀스이면 true를 반환하고 그렇지 않으면 false를 반환

- [392. Is Subsequence](https://leetcode.com/problems/is-subsequence/)

```java
class Solution {
    
    // 부분 문자열인지 체크 
    // Two Pointer: 부분문자열의 길이가 될때까지 동일문자를 체크한다.
    // T: O(n)
    public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) return true;
        
        int indexS = 0, indexT = 0;
        
        while (indexT < t.length()) {
            // 동일한 문자이면 부분문자열의 인덱스를 증가 시킨다. 
            if (t.charAt(indexT) == s.charAt(indexS)) {
                indexS++;
                // 존재하는 문자의 개수가 문자열 길이와 같으면 부분문자열이다.
                if (indexS == s.length()) {
                    return true;
                }
            }
            
            indexT++;
        }
        
        return false;
    }
}
```
