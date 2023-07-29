---
layout: post
published: true
title: "1056. Confusing Number"
categories: interview
tags: easy math
---

> 정수 n이 주어지면 혼란스러운 숫자이면 true를 반환하고 그렇지 않으면 false를 반환

[1056. Confusing Number](https://leetcode.com/problems/confusing-number/)

```java
class Solution {
    public boolean confusingNumber(int n) {
        Map<Integer, Integer> map = new HashMap<>();
        
        map.put(6, 9);
        map.put(9, 6);
        map.put(0, 0);
        map.put(1, 1);
        map.put(8, 8); 
        
        int rotating = 0;
        int x = n;
        while (x != 0) {
            int remainder = x % 10;
            if (!map.containsKey(remainder)) return false;
            //if (rotating > Integer.MAX_VALUE / 10) return false;
            // 뒤집은 숫자를 더한다.
            rotating = rotating * 10 + map.get(remainder);
            // 다은 자리로 넘어간다.
            x /= 10;
        }    
        
        return n == rotating? false: true;
    }
}
```