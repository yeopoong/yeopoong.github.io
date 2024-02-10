---
layout: post
published: true
title: "168. Excel Sheet Column Title"
categories: interview
tags: easy math
---

> 정수 columnNumber가 주어지면 Excel 시트에 나타나는 해당 열 제목을 반환합니다.

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