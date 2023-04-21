---
layout: post
published: true
title: "139. Word Break"
categories: interview
tags: problems backtracking
---

> 문자 보드의 m x n 그리드와 문자열 단어가 주어지면 단어가 그리드에 있으면 true를 반환

-[79. Word Search](https://leetcode.com/problems/word-search/)

```java
class Solution {
    
    // 단어 검색
    public boolean exist(char[][] board, String word) {
        for (int r = 0; r < board.length; r++) {
            for (int c = 0; c < board[r].length; c++) {
                if (exist(board, r, c, word, 0)) return true;
            }
        }
        
        return false;
    }

    // Backtracking (DFS)
    // T: O(N*4^L) N: the number of cells, L: the length of the word
    // S: O(L)
    private boolean exist(char[][] board, int r, int c, String word, int i) {
        if (i == word.length()) return true;
        
        // Check the boundaries
        if (r < 0 || c < 0 || r == board.length || c == board[r].length || board[r][c] != word.charAt(i)) return false;
        
        // 동일한 문자 셀은 두 번 이상 사용할 수 없다.
        // Set this board position to seen.
        board[r][c] ^= 256;
        
        // 상하좌우 체크
        boolean exist = exist(board, r+1, c, word, i+1)
                     || exist(board, r-1, c, word, i+1)
                     || exist(board, r, c-1, word, i+1)
                     || exist(board, r, c+1, word, i+1);
        
        board[r][c] ^= 256;
        
        return exist;
    }
}
```