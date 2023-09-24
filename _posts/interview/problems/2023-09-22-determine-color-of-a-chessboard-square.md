---
layout: post
published: true
title: "1812. Determine Color of a Chessboard Square"
categories: interview
tags: easy string
---

> 체스판 사각형의 좌표를 나타내는 문자열이 주어지면 사각형이 흰색이면 true를 반환하고 사각형이 검은색이면 false를 반환합니다.

![](https://assets.leetcode.com/uploads/2021/02/19/screenshot-2021-02-20-at-22159-pm.png)

[1812. Determine Color of a Chessboard Square](https://leetcode.com/problems/determine-color-of-a-chessboard-square/)

```java
class Solution {
    public boolean squareIsWhite(String coordinates) {
        char letter = coordinates.charAt(0);
        int digit = coordinates.charAt(1) - '0';
        
        if (letter == 'a' || letter == 'c' || letter == 'e' || letter == 'g') { 
            return digit % 2 == 0; // when digit is even
        } else { 
            return digit % 2 == 1; // when digit is odd
        }
    }
}
```