---
layout: post
published: true
title: "200. Number of Islands"
categories: interview
tags: medium graph dfs bfs
---

> '1'(땅)과 '0'(물)의 지도를 나타내는 m x n 2D 이진 그리드가 주어지면 섬의 수를 반환

[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

각 셀을 순차적으로 방문하면서 땅일 경우 인접한 상하좌우셀을 모두 방문하고 방문처리한다.

DFS Solution
```java
class Solution {
    char[][] g;
    
    // O(m*n)
    public int numIslands(char[][] grid) {
        int count = 0;
        
        g = grid;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                count += dfs(i, j);
            }
        }
        
        return count;
    }
    
    private int dfs(int i, int j) {
        if (i < 0 || i == g.length || j < 0 || j == g[i].length || g[i][j] == '0') {
            return 0;
        }
        
        g[i][j] = '0';
        
        // 인접한 상하좌우 모든 셀을 방문처리
        dfs(i+1,   j); 
        dfs(i-1,   j); 
        dfs(i,   j+1); 
        dfs(i,   j-1);
        
        return 1;
    }
}
```

BFS Solution
```java
class Solution {
    char[][] g;
    
    // O(m*n)
    public int numIslands(char[][] grid) {
        int count = 0;
        
        g = grid;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == '1') {
                    bfs(i, j);
                    count++;
                }
            }
        }
        
        return count;
    }
    
    private void bfs(int i, int j) {
        
        g[i][j] = '0';
        Queue<int[]> q = new LinkedList();
        q.offer(new int[]{i, j});
        
         // 상하좌우
        int[][] directions = { {1, 0}, {-1, 0}, {0, 1}, {0, -1} };

        while (!q.isEmpty()) {
            int[] curr = q.poll();
            // 값이 0인 셀의 인접한 상하좌우 셀을 처리한다.
            for (int[] dir : directions) {
                int x = curr[0] + dir[0], y = curr[1] + dir[1];
                // 경계조건 및 처리여부 체크
                if (x < 0 || x == g.length || y < 0 || y == g[i].length || g[x][y] == '0') continue;
                // 인접 셀 처리를 하기 위해서 큐에 넣는다.
                q.offer(new int[]{x, y});
                g[x][y] = '0';
            }
        }
    }
}
```