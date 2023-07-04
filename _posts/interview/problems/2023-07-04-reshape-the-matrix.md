---
layout: post
published: true
title: "566. Reshape the Matrix"
categories: interview
tags: easy matrix
---

> MATLAB에는 m x n 행렬을 원래 데이터를 유지하면서 r x c 크기가 다른 새 행렬로 재구성

[566. Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)

```java
class Solution {

    // T: O(mn)
    public int[][] matrixReshape(int[][] mat, int r, int c) {
        int m = mat.length;
        int n = mat[0].length;
		
        // Check whether the matrix can be made by using the given r,c values.
        if (m * n != r * c) return mat;
        
		// Store in 1-d Array.
        int[] arr = new int[m * n];
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                arr[count++] = mat[i][j];
            }
        }
                
		// Initilize a new Matrix with given Dimensions
        int[][] reshape = new int[r][c];
        count = 0;
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                reshape[i][j] = arr[count++];
            }
        }
                
        return reshape;
    }
}
```