---
layout: post
published: true
title: "695. Max Area of Island"
categories: interview
tags: medium dfs
---

> 그리드에서 섬의 ​​최대 면적을 반환: 섬의 면적은 섬에서 값이 1인 셀의 수

[695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)

![](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)

```java
class Solution {
    
    // 그리드에서 섬의 최대 면적을 반환
    // Time Complexity: O(R * C)
    // Space Complexity: O(R * C)
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                // 섬일 경우에 DFS 탐색한다.
                if (grid[i][j] == 1) {
                    // 현재 그룹의 갯수를 최대값과 비교한다.
                    maxArea = Math.max(dfs(i, j, grid), maxArea);
                }
            }
        }
                    
        return maxArea;
    }
    
    // 연결된 육지를 방문하고 방문처리(0) 한다.
    public int dfs(int i, int j, int[][] grid) {
        if (i < 0 || j < 0 || i == grid.length || j == grid[i].length || grid[i][j] == 0) {
            return 0;
        }

        grid[i][j] = 0;

        // 상하좌우로 재귀호출하면서 1(land)의 갯수를 합해서 리턴한다.
        int up    = dfs(i+1, j, grid);
        int down  = dfs(i-1, j, grid);
        int left  = dfs(i, j-1, grid);
        int right = dfs(i, j+1, grid);

        return up + down + left + right + 1;
    }
}
```