---
layout: post
published: true
title: "390. Elimination Game"
categories: interview
tags: problems math recursion
---

> 증가하는 순서로 정렬된 [1, n] 범위의 모든 정수 목록에서 하나의 숫자가 남을 때까지 왼쪽에서 오른쪽으로, 오른쪽에서 왼쪽으로 번갈아 가며 삭제

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
