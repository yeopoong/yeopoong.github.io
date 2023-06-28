---
layout: post
published: true
title: "567. Permutation in String"
categories: interview
tags: medium string
---

> 두 개의 문자열 s1과 s2가 주어지면 s2에 s1의 순열이 포함되어 있으면 true를 반환하고 그렇지 않으면 false를 반환

[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

```java
class Solution {
    // 문자열이 다른 문자열의 순열 중 하나를 포함하는지 체크
    // O(n)
    public boolean checkInclusion(String s1, String s2) {
        int len1 = s1.length(), len2 = s2.length();
        
        if (len1 > len2) return false;
        
        int[] count = new int[26];
        
        // 처음 S1 문자열의 길이 만큼 문자 출현 횟수를 구한다.
        for (int i = 0; i < len1; i++) {
            count[s1.charAt(i) - 'a']++;
            count[s2.charAt(i) - 'a']--;
        }
        
        // 카운트가 모두 제로이면 S1==S2 
        if (allZero(count)) return true;
        
        // Sliding window
        // S1 문자길이 다음 문자부터 시작
        for (int start = len1; start < len2; start++) {
            // S2 문자를 체크하므로 카운트는 감소 시켜야 한다.
            count[s2.charAt(start) - 'a']--;
            
            // * 연속문자열을 체크해야 하므로 이전 문자 카운트는 증가시켜야 카운트 체크를 할 수 있다.
            count[s2.charAt(start - len1) - 'a']++;
            
            if (allZero(count)) return true;
        }
        
        return false;
    }
    
    private boolean allZero(int[] count) {
        for (int i = 0; i < 26; i++) {
            if (count[i] != 0) return false;
        }
        
        return true;
    }
}
```