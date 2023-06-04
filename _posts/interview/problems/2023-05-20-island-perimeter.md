---
layout: post
published: true
title: "463. Island Perimeter"
categories: interview
tags: graph matrix
---

> 섬의 둘레를 결정

- [463. Island Perimeter](https://leetcode.com/problems/island-perimeter/)

![](https://assets.leetcode.com/uploads/2018/10/12/island.png)

```java
class Solution {
    
    // 섬의 둘레을 계산
    // T: O(row*com)
    // loop over the matrix and count the number of islands;
    // if the current dot is an island, count if it has any right neighbour or down neighbour;
    // the result is islands * 4 - neighbours * 2
    public int islandPerimeter(int[][] grid) {
        int islands = 0, neighbours = 0;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    islands++; // count islands
                    if (i < grid.length - 1 && grid[i + 1][j] == 1) neighbours++; // count down neighbours
                    if (j < grid[i].length - 1 && grid[i][j + 1] == 1) neighbours++; // count right neighbours
                }
            }
        }

        return islands * 4 - neighbours * 2;
    }
}
```