---
layout: post
published: true
title: "422. Valid Word Square"
categories: interview
tags: easy palindrome
---

> 문자열 단어 배열이 주어지면 유효한 단어 사각형을 형성하는 경우 true를 반환

[422. Valid Word Square](https://leetcode.com/problems/valid-word-square/)

![](https://assets.leetcode.com/uploads/2021/04/09/validsq1-grid.jpg)

```java
class Solution {
    
    public boolean validWordSquare(List<String> words) {
        if (words == null || words.size() == 0) {
            return true;
        }
        
        int n = words.size();
        
        for (int i=0; i<n; i++) {
            for (int j=0; j<words.get(i).length(); j++) {
                if (j >= n || words.get(j).length() <= i || words.get(j).charAt(i) != words.get(i).charAt(j)) {
                    return false;
                }
            }
        }
        
        return true;
    }
}
```