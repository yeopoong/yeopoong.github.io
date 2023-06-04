---
layout: post
published: true
title: "723. Candy Crush"
categories: interview
tags: array two-pointers simulation
---

> Candy Crush의 기본 제거 알고리즘 구현  
> 1. 같은 종류의 사탕이 3개 이상 수직 또는 수평으로 인접해 있으면 동시에 모두 부수십시오. 이 위치는 비어 있게 됩니다.  
> 2. 모든 사탕을 동시에 부순 후 보드의 빈 공간에 사탕이 있으면 이 사탕은 동시에 사탕이나 바닥에 닿을 때까지 떨어집니다. 새로운 사탕은 상단 경계 밖으로 떨어지지 않습니다.  
> 3. 위의 단계 후에 부술 수 있는 사탕이 더 많이 존재할 수 있습니다. 그렇다면 위의 단계를 반복  
> 4. 부술 수 있는 사탕이 더 이상 존재하지 않으면(즉, 보드가 안정적이면) 현재 보드를 반환  
> 보드가 안정될 때까지 위의 규칙을 수행한 다음 안정적인 보드를 반환  

- [723. Candy Crush](https://leetcode.com/problems/candy-crush/)

![](https://assets.leetcode.com/uploads/2018/10/12/candy_crush_example_2.png)

```java
class Solution {
    
    public int[][] candyCrush(int[][] board) {
      int m = board.length;
      int n = board[0].length;

      boolean shouldContinue = false;

      // Crush horizontally
      for (int i = 0; i < m; i++) {
        for (int j = 0; j < n - 2; j++) {
          int v = Math.abs(board[i][j]);
          if (v > 0 && v == Math.abs(board[i][j + 1]) && v == Math.abs(board[i][j + 2])) {
            board[i][j] = board[i][j + 1] = board[i][j + 2] = -v;
            shouldContinue = true;
          }
        }
      }

      // Crush vertically
      for (int i = 0; i < m - 2; i++) {
        for (int j = 0; j < n; j++) {
          int v = Math.abs(board[i][j]);
          if (v > 0 && v == Math.abs(board[i + 1][j]) && v == Math.abs(board[i + 2][j])) {
            board[i][j] = board[i + 1][j] = board[i + 2][j] = -v;
            shouldContinue = true;
          }
        }
      }

      // Drop vertically
      for (int j = 0; j < n; j++) {
        int r = m - 1;
        for (int i = m - 1; i >= 0; i--) {
          if (board[i][j] >= 0) {
            board[r--][j] = board[i][j];
          }
        }
        for (int i = r; i >= 0; i--) {
          board[i][j] = 0;
        }
      }

      return shouldContinue ? candyCrush(board) : board;
    }
}
```