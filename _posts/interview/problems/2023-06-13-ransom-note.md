---
layout: post
published: true
title: "383. Ransom Note"
categories: interview
tags: easy string hashmap
---

> ansomNote와 magazine이라는 두 개의 문자열이 주어지면, magazine의 문자를 사용하여 ransomNote를 구성할 수 있으면 true를 반환하고 그렇지 않으면 false를 반환

[383. Ransom Note](https://leetcode.com/problems/ransom-note/)

```java
class Solution {
    // 특정 문자열에서 다른 문자열을 만들 수 있는지 체크
    // O(n)
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] arr = new int[26];
        
        // 원본 문자의 개수 카운트
        for (int i = 0; i < magazine.length(); i++) {
            arr[magazine.charAt(i) - 'a']++;
        }
        
        for (int i = 0; i < ransomNote.length(); i++) {
            // 만들려는 문자의 개수가 원본 문자열보다 많으면 불가능
            if (--arr[ransomNote.charAt(i) - 'a'] < 0) {
                return false;
            }
        }
        
        return true;
    }
}
```
