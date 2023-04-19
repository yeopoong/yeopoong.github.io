---
layout: post
published: true
title: "1347. Minimum Number of Steps to Make Two Strings Anagram"
categories: interview
tags: problems hashmap
---

> t를 s의 애너그램으로 만들기 위한 최소 단계 수를 반환

- [1347. Minimum Number of Steps to Make Two Strings Anagram](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)

```java
class Solution {
    public int minSteps(String s, String t) {
        int steps = 0;
        
        int[] count = new int[26];
        
        for (int i = 0; i < s.length(); ++i) {
            ++count[s.charAt(i) - 'a']; // count the occurrences of chars in s.
            --count[t.charAt(i) - 'a']; // compute the difference between s and t.
        }
        
        for (int step : count) {
            if (step > 0) {
                steps += step;
            }
        }
        
        // return Arrays.stream(count).map(Math::abs).sum() / 2; 
        // return Arrays.stream(count).filter(i -> i > 0).sum();
        
	    return steps;
    }
}
```