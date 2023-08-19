---
layout: post
published: true
title: "1100. Find K-Length Substrings With No Repeated Characters"
categories: interview
tags: medium two-pointers
---

> 문자열 s와 정수 k가 주어지면 반복되는 문자가 없는 k 길이의 하위 문자열의 수를 반환

[1100. Find K-Length Substrings With No Repeated Characters](https://leetcode.com/problems/find-k-length-substrings-with-no-repeated-characters/)

```java
class Solution {
    public int numKLenSubstrNoRepeats(String s, int k) {
        int res = 0;
        
        Set<Character> set = new HashSet<>();
        int i = 0;
        
        for (int j = 0; j < s.length(); ++j) {
            // 반복 문자가 존재하면 앞에서 부터 해당문자까지 제거한다.
            while (set.contains(s.charAt(j))) {
                //System.out.println(s.charAt(j) + ":" + set);
                set.remove(s.charAt(i++));
            }
            set.add(s.charAt(j));
            // 문자열 길이가 K가 되면 카운트 증가하고 가장 앞문자 제거
            if (j - i + 1 == k) {
                res++;
                set.remove(s.charAt(i++));
            }
        }
        
        return res;
    }
}
```