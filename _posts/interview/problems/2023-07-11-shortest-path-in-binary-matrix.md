---
layout: post
published: true
title: "1091. Shortest Path in Binary Matrix"
categories: interview
tags: medium matrix dfs
---

> n x n 이진 행렬 그리드가 주어지면 행렬에서 가장 짧은 클리어 경로의 길이를 반환

[1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

![](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)

```java
class Solution {
    
    class Pair {
        int x;
        int y;
        int count;

        Pair(int x, int y, int count) {
            this.x = x;
            this.y = y;
            this.count = count;
        }
    }
    
    // 최단 경로의 길이를 반환: 경로의 모든 인접한 셀은 8방향으로 연결
    public int shortestPathBinaryMatrix(int[][] grid) {
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(0, 0, 1));

        while (queue.size() > 0) {
            Pair rem = queue.remove();
            
            int x = rem.x;
            int y = rem.y;
            int count = rem.count;
            
            // 경로의 모든 방문한 셀은 0
            if (x >= 0 && y >= 0 && x < grid.length && y < grid[0].length && grid[x][y] == 0) {
                // 방문처리를 한다.
                grid[x][y] = 1;
                
                // bottom-right 지점에 도착하면 현재까지 경로의 길이를 리턴한다.
                if (x == grid.length - 1 && y == grid[0].length - 1) return count;

                // 8가지 방향의 경로를 큐에 추가한다.
                queue.add(new Pair(x - 1, y,     count + 1));
                queue.add(new Pair(x - 1, y + 1, count + 1));
                queue.add(new Pair(x,     y + 1, count + 1));
                queue.add(new Pair(x + 1, y + 1, count + 1));
                queue.add(new Pair(x + 1, y,     count + 1));
                queue.add(new Pair(x + 1, y - 1, count + 1));
                queue.add(new Pair(x,     y - 1, count + 1));
                queue.add(new Pair(x - 1, y - 1, count + 1));
            }
        }
        
        return -1;
    }
}
```