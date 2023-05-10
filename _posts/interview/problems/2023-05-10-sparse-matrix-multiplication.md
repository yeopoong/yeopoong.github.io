---
layout: post
published: true
title: "311. Sparse Matrix Multiplication"
categories: interview
tags: problems array hashmap matrix
---

> 크기 m x k의 두 희소 행렬 mat1과 크기 k x n의 mat2가 주어지면 mat1 x mat2의 결과를 반환  
> - 행렬 곱셈은 두 행렬이 곱해질 때 다른 행렬이 출력되는 이진 연산
> - 결과 행렬의 크기는 다음과 같습니다. (A의 행 수 × B의 열 수)

- [311. Sparse Matrix Multiplication](https://leetcode.com/problems/sparse-matrix-multiplication/)

- 희소 행렬(Sparse Matrix)은 행렬의 원소 중에 많은 항들이 '0'으로 구성되어 있는 행렬

![](https://assets.leetcode.com/uploads/2021/03/12/mult-grid.jpg)

```java
class Solution {
    
    // 희소행렬
    public int[][] multiply(int[][] mat1, int[][] mat2) {
        int m = mat1.length, n = mat2[0].length;
        
        int[][] prd = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int k = 0; k < mat1[i].length; k++) {
                if (mat1[i][k] != 0) {
                    for (int j = 0; j < n; j++) {
                        if (mat2[k][j] != 0) prd[i][j] += mat1[i][k] * mat2[k][j];
                    }
                }
            }
        }
        
        return prd;   
    }
}
```