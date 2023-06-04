---
layout: post
published: true
title: "13. Roman to Integer"
categories: interview
tags: hashmap
---

> 로마 숫자가 주어지면 정수로 변환

- [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

```java
class Solution {

    static Map<Character, Integer> values = new HashMap<>();
    
    static {
        values.put('M', 1000);
        values.put('D', 500);
        values.put('C', 100);
        values.put('L', 50);
        values.put('X', 10);
        values.put('V', 5);
        values.put('I', 1);
    }
    
    // 로마 숫자가 주어지면 정수로 변환
    // largest to smallest: add them up
    // smaller before larger: subtract smaller
    // T: O(n)
    public int romanToInt(String s) {
        int sum = 0;
        
        // 마지막 값은 다음값이 없기 때문에 처리하지 않는다.
        for (int i = 0; i < s.length() - 1; i++) {
            int value = values.get(s.charAt(i));
            
            // I,X,C 일 경우 미리 값을 빼놓는다(다음문자에서 보충됨) 
            if (value < values.get(s.charAt(i+1))) {
                sum -= value;
            } else {
                sum += value;
            }
        }
        
        // 마지막 값을 처리한다.
        return sum + values.get(s.charAt(s.length() - 1));
    }
}
```