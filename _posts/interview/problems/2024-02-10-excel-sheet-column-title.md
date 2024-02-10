---
layout: post
published: true
title: "168. Excel Sheet Column Title"
categories: interview
tags: easy math
---

> 두 개의 정수 n과 k가 주어지면 [1, n] 범위에서 선택한 k 숫자의 가능한 모든 조합을 반환합니다.

[168. Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

```java
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder ans = new StringBuilder();
        
        while (columnNumber > 0) {
            columnNumber--;
            // Get the last character and append it at the end of the string.
            ans.append((char) (columnNumber % 26 + 'A'));
            columnNumber = columnNumber / 26;
        }
        
        // Reverse it, as we appended characters in reverse order.
        return ans.reverse().toString();
    }
}
```