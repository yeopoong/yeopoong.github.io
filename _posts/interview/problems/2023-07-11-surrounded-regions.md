---
layout: post
published: true
title: "130. Surrounded Regions"
categories: interview
tags: medium tree dfs
---

> 'X'와 'O'가 포함된 m x n 매트릭스 보드가 주어지면 'X'로 둘러싸인 4방향 영역을 모두 캡처합니다.

[130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

```java
class Solution {
    
    // Capture surrounded regions -> Capture evetything except unsurrounded regions
    // O(n*m)
    public void solve(char[][] board) {
        int m = board.length;
        int n = board[0].length;
        
        // 1. Capture unsurrounded regions (O -> T)
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O' && (i == 0 || i == m - 1) || (j == 0 || j == n -1))  {
                    capture(board, i, j);
                }
            }
        }
        
        // 2. Capture surrounded regions (O -> X)
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O')  {
                    board[i][j] = 'X';
                }
            }
        }
        
        // 3. Uncapture unsurrounded regions (T -> O)
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'T') {
                    board[i][j] = 'O';
                }
            }
        }
    }
    
    // DFS: O -> T
    private void capture(char[][] board, int r, int c) {
        if (r < 0 || c < 0 || r == board.length || c == board[0].length || board[r][c] != 'O') return;
        
        board[r][c] = 'T';
        
        // 상하좌우 처리
        capture(board, r + 1, c);
        capture(board, r - 1, c);
        capture(board, r, c + 1);
        capture(board, r, c - 1);
    }
}
```