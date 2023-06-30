---
layout: post
published: true
title: "994. Rotting Oranges"
categories: interview
tags: medium bfs
---

> 각 셀이 세 가지 값 중 하나를 가질 수 있는 m x n 그리드가 제공되고  
> 썩은 오렌지에 4방향으로 인접한 신선한 오렌지는 1분마다 썩게 될때,  
> 셀에 신선한 오렌지가 없을 때까지 경과해야 하는 최소 시간(분)을 반환

[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

```java
class Solution {
    
    // rotten orange
    Queue<int[]> queue = new LinkedList<>();
    
    // fresh orange
    int fresh = 0;
            
    // O(n * m)
    public int orangesRotting(int[][] grid) {
        
        int minutes = 0;
        
		// find all fresh and rotten oranges
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                int[] cell = new int[] {i, j};
                if (grid[i][j] == 1) {
                    fresh += 1;
                } else if (grid[i][j] == 2) {
                    queue.offer(cell);
                }
            }
        } 
        
		// BFS Iteration
        while (fresh > 0 && !queue.isEmpty()) {
            minutes++;
            
            int size = queue.size();
            // 시작지점은 썩은 오랜지 모두에서 체크해야 한다.
            for (int r = 0; r < size; r++) {
                int[] rotten = queue.poll(); 
                int i = rotten[0], j = rotten[1];
                rotAdjacent(grid, i - 1, j);
                rotAdjacent(grid, i + 1, j);
                rotAdjacent(grid, i, j - 1);
                rotAdjacent(grid, i, j + 1);
            }
        }
                        
		// check if fresh oranges remain and return accordingly
        return fresh == 0 ? minutes : - 1;
    }
    
    private void rotAdjacent(int[][] grid, int i, int j) {
        // 유효한 셀이고 신선한 오랜지만 처리한다.
        if (i < 0 || i == grid.length  || j < 0 || j == grid[0].length  || grid[i][j] != 1) return;
        
        grid[i][j] = 2; // 썩은 오랜지로 만들고
        queue.offer(new int[] {i, j}); // 큐에 넣고
        fresh -= 1; // 신선한 오랜지 카운트를 감소시킨다. 
    }
}
```