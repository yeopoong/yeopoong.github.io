---
layout: post
published: false
title: "76. Minimum Window Substring"
categories: interview
tags: interview sliding-window
---

- [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

```java
class Solution {
    
    // 모든 문자를 포함하는 최소길이 윈도우 문자열
    // T: O(m + n)
    public String minWindow(String s, String t) {
        int[] need = new int[128];
        
        for (char c : t.toCharArray()) need[c]++;
        
        // current window two pointer
        int l = 0, r = 0; 
        
        // minimum window two pointer
        int i = 0, j = 0;
        
        int missing = t.length();
        
        while (r < s.length()) {
            // 문자가 부분문자열에 포함되면 
            if (need[s.charAt(r)] > 0) missing--;
            need[s.charAt(r)]--;
            r++;
            
            // 모든 문자를 포함하는 윈도우일 경우
            while (missing == 0) {
                // 이전 윈도우 길이보다 작으면 새로운 윈도우 인덱스로 업데이트
                if (j == 0 || (r - l) < (j - i)) {
                    j = r;
                    i = l;
                }
                // 윈도우 시작 지점을 오른쪽으로 이동한다.
                need[s.charAt(l)]++;
                // 문자가 부분문자열에 포함되면 (중복문자를 처리하기 위함) 
                if (need[s.charAt(l)] > 0) missing++;
                l++;
            }
        }
        
        return s.substring(i, j);
    }
}
```