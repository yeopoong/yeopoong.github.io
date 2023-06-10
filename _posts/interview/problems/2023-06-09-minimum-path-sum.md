---
layout: post
published: true
title: "64. Minimum Path Sum"
categories: interview
tags: array matrix dynamic-programming
---

> 음수가 아닌 숫자로 채워진 m x n 그리드가 주어지면 왼쪽 위에서 오른쪽 아래로 경로를 따라 모든 숫자의 합을 최소화하는 경로를 찾습니다.

[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```java
class Solution {
    // 경로를 따라 모든 숫자의 합을 최소화하는 왼쪽 위에서 오른쪽 아래로 경로
    // 아래 또는 오른쪽으로만 이동할 수 있다.
    // T: O(mn)
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        
        int[][] dp = new int[m + 1][n + 1];
        for (int[] row: dp) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        dp[m - 1][n] = 0;
        
        for (int r = m - 1; r >= 0; r--) {
            for (int c = n - 1; c >= 0; c--) {
                dp[r][c] = grid[r][c] + Math.min(dp[r + 1][c], dp[r][c + 1]);
            }
        }
        
        return dp[0][0];
    }
}
```
