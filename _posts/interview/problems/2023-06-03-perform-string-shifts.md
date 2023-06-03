---
layout: post
published: true
title: "1427. Perform String Shifts"
categories: interview
tags: problems string
---

> 다음 연산의 리스트에 따라서 문자열 이동한 결과를 리턴
> shift[i] = [direction, amount]

- [1427. Perform String Shifts](https://leetcode.com/problems/perform-string-shifts/)

```java
class Solution {
    
    // 문자열 이동
    public String stringShift(String s, int[][] shift) {
        int len = s.length();
        
        for (int[] move : shift) {
            int direction = move[0];
            int amount = move[1] % len;
            
            // for left shift
            if (direction == 0) {
                // Move necessary amount of characters from front to end 
                s = s.substring(amount) + s.substring(0, amount);
            // for right shift
            } else {
                // Move necessary amount of characters from end to front
                s = s.substring(len - amount) + s.substring(0, len - amount);
            }
        }
        
        return s;
    }
}
```
