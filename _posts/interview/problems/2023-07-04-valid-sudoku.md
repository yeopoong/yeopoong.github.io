---
layout: post
published: true
title: "36. Valid Sudoku"
categories: interview
tags: mediumn array hashmap
---

> 9 x 9 스도쿠 보드가 유효한지 확인

[36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

Set 자료구조를 사용하여 행, 열, 블록에 대한 중복 체크를 한다.

```java
class Solution {
	// combined method to check if a number possible to a row,col position is ok
    // O(n^2)
    public boolean isValidSudoku(char[][] board) {
        // 중복 체크를 위해서 집합 자료구조를 사용
        Set seen = new HashSet();
        
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                char number = board[i][j];
                // 숫자일 경우만 체크
                if (number != '.') {
                    // 각 행,열,블록(키워들 붙여서 각 집합을 구분) 에 대해서 중복 여부를 체크한다
                    // 셋중에 어떤 것도 중복이 발생하면 유효하지 않다.
                    if (!seen.add(number + " in row " + i) ||
                        !seen.add(number + " in column " + j) ||
                        !seen.add(number + " in block " + i / 3 + "-" + j / 3))
                        return false;
                }
            }
        }
        
        return true;
    }
}
```