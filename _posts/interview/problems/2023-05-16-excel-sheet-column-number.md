---
layout: post
published: true
title: "171. Excel Sheet Column Number"
categories: interview
tags: string math
---

> Excel 시트에 표시되는 열 제목을 나타내는 문자열 columnTitle이 주어지면 해당 열 번호를 반환

- [171. Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number/)

```java
class Solution {
    
    // Left to Right
    // ex> "LEET"
    // L = 12
    // E = (12 x 26) + 5 = 317
    // E = (317 x 26) + 5 = 8247
    // T = (8247 x 26) + 20 = 214442
    // T: O(n)
    public int titleToNumber(String columnTitle) {
        int result = 0;
        
        for (int i = 0; i < columnTitle.length(); i++) {
            result = result * 26;
            // subtracting characters is subtracting ASCII values of characters
            result += (columnTitle.charAt(i) - 'A' + 1);
        }
        
        return result;
    }
}
```