---
layout: post
published: true
title: "74. Search a 2D Matrix"
categories: interview
tags: medium binary-search
---

> 정수 대상이 주어지면 대상이 행렬에 있으면 true를 반환하고 그렇지 않으면 false를 반환  

[74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```java
class Solution {
    // O(log(m*n))
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = matrix.length;
        int col = matrix[0].length;
        
        // 이진검색
        int left = 0, right = row * col - 1;
        
        while (left <= right) {
            int pivot = left + (right - left) / 2;
            // *컬럼개수로 나눈 몫이 행, 나머지가 열이 된다.
		    int value = matrix[pivot/col][pivot%col];
            
            if (value < target) {
                left = pivot + 1;
            } else if (value > target) {
                right = pivot - 1;
            } else {
                return true;
            }
        }
        
        return false;
    }
}
```
