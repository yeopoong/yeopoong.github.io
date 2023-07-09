---
layout: post
published: true
title: "438. Find All Anagrams in a String"
categories: interview
tags: medium sliding-window
---

> 두 개의 문자열 s와 p가 주어지면 s에 있는 p의 애너그램의 모든 시작 인덱스의 배열을 반환

[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

```java
class Solution {
    // 문자열에서 모든 아나그램 찾기
    // O(s)
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> list = new ArrayList<>();
        
        int[] cnt = new int[128];
        
        for (char c : p.toCharArray()) cnt[c]++;
        
        // Sliding Window with two pointers
        for (int l = 0, r = 0; r < s.length(); ++r) {
            char c = s.charAt(r);
            cnt[c]--;
            
            // 매칭되지 않으면
            while (cnt[c] < 0) { 
                // 매칭값을 원복 시키고
                cnt[s.charAt(l)]++; 
                // 왼쪽 포인터를 이동한다.
                l++;
            }
            
            // 문자열의 길이가 아나그램 문자열 길이와 같으면 p's anagram 이다. 
            if (r - l + 1 == p.length()) { 
                list.add(l);  // 시작 인덱스를 결과 리스트에 추가한다. 
            }
        }
        
        return list; 
    }
}
```