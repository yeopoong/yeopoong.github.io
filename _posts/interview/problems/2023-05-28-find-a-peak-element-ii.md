---
layout: post
published: true
title: "1901. Find a Peak Element II"
categories: interview
tags: problems binary-search array matrix
---

> 2개의 인접한 셀이 같지 않은 m x n 행렬 mat가 주어지면 임의의 피크 요소 mat[i][j]를 찾아 길이 배열 [i,j]를 반환

- [1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/)

![](https://assets.leetcode.com/uploads/2021/06/08/1.png)

```java
class Solution {
    
    // 인접한 모든 이웃보다 큰 요소 찾기
    // T: O(n log(m))
    public int[] findPeakGrid(int[][] mat) {
        int startCol = 0, endCol = mat[0].length-1;
        
        while (startCol <= endCol) {
            int maxRow = 0, midCol = startCol + (endCol-startCol) / 2;
            
            for (int row = 0; row < mat.length; row++) {
                 maxRow = mat[row][midCol] >= mat[maxRow][midCol]? row : maxRow;  
            }
            
            boolean leftIsBig    =   midCol-1 >= startCol  &&  mat[maxRow][midCol-1] > mat[maxRow][midCol];
            boolean rightIsBig   =   midCol+1 <= endCol    &&  mat[maxRow][midCol+1] > mat[maxRow][midCol];
            
            if (rightIsBig) {        // there is an element in 'right' that is bigger than all the elements in the 'midCol' 
                startCol = midCol+1; // so 'midCol' cannot have a 'peakPlane'
            } else if (leftIsBig) {  
                endCol = midCol-1;
            } else {
                return new int[]{maxRow, midCol};
            }
        }
        
        return null;
    }
}
```