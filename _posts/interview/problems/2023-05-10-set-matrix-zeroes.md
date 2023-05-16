---
layout: post
published: true
title: "73. Set Matrix Zeroes"
categories: interview
tags: problems array hashmap matrix
---

> m x n 정수 행렬이 주어지면 요소가 0이면 전체 행과 열을 0으로 설정

- [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```java
class Solution {
    
    // m x n 정수 행렬이 주어지면 요소가 0이면 전체 행과 열을 0으로 설정
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        
        boolean firstRow = false;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    if (i == 0) {
                        firstRow = true;
                    } else {
                        matrix[i][0] = 0;
                    }
                }
            }
        }

        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (matrix[0][0] == 0) {
            for (int i = 0; i < rows; i++) {
                matrix[i][0] = 0;
            }
        }

        if (firstRow) {
            for (int j = 0; j < cols; j++) {
                matrix[0][j] = 0;
            }
        }
    }
}
```