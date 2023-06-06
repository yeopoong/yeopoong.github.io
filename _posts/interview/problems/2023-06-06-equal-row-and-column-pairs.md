---
layout: post
published: true
title: "2352. Equal Row and Column Pairs"
categories: interview
tags: hashmap
---

> n x n 정수 행렬 그리드가 주어지면 행 ri와 열 cj가 같은 쌍(ri, cj)의 수를 반환  
> - 행과 열 쌍은 동일한 순서로 동일한 요소를 포함하는 경우(즉, 동일한 배열) 동일한 것으로 간주

[2352. Equal Row and Column Pairs](https://leetcode.com/problems/equal-row-and-column-pairs/)

![](https://assets.leetcode.com/uploads/2022/06/01/ex2.jpg)

```java
class Solution {
    
    // 동일한 행 및 열 쌍
    // T: O(n^2)
    public int equalPairs(int[][] grid) {
        int cnt = 0;
        
        HashMap<String, Integer> map = new HashMap<>();
        
        int row = grid.length;
        int col = grid.length;
        
        // Row to Column
        for (int i = 0; i < row; i++) {
            String res = "";
            for (int j = 0; j < col; j++) {
                res += "-" + grid[i][j];
            }
            map.put(res, map.getOrDefault(res, 0) + 1);
        }
        
        // map: {-3-2-1=1, -1-7-6=1, -2-7-7=1}
        
        // Column to Row
        for (int j = 0; j < col; j++) {
            String res = "";
            for (int i = 0; i < row; i++) {
                res += "-" + grid[i][j];
            }
            cnt += map.getOrDefault(res, 0);
        }
        
        return cnt;
    }
}
```