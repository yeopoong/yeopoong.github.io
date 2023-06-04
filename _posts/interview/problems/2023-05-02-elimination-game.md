---
layout: post
published: true
title: "390. Elimination Game"
categories: interview
tags: linked-list
---

> 정수 n이 주어지면 배열에 남아 있는 마지막 숫자를 반환

- [390. Elimination Game](https://leetcode.com/problems/elimination-game/)

```java
class Solution {
    
    public int lastRemaining(int n) {
        int head = 1;
        
        boolean left = true;
        int remaining = n;
        int step = 1;
        
        while (remaining > 1) {
            if (left || remaining % 2 ==1) {
                head = head + step;
            }
            remaining = remaining / 2;
            step = step * 2;
            left = !left;
        }
        
        return head;
    }
}
```
