---
layout: post
published: true
title: "1901. Find a Peak Element II"
categories: interview
tags: problems matrix binary-search
---

> 문자열을 반전시키는 함수를 작성  
> 입력 문자열은 문자 배열로 제공

- [1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/)

```java
class Solution {
    
    // 인접한 모든 이웃보다 큰 요소 찾기
    public int[] findPeakGrid(int[][] mat) {
        int startCol = 0, endCol = mat[0].length-1;
        
        while (startCol <= endCol) {
            int maxRow = 0, midCol = startCol + (endCol-startCol) / 2;
            
            for (int row=0; row<mat.length; row++) {
                 maxRow = mat[row][midCol] >= mat[maxRow][midCol]? row : maxRow;  
            }
            
            boolean leftIsBig    =   midCol-1 >= startCol  &&  mat[maxRow][midCol-1] > mat[maxRow][midCol];
            boolean rightIsBig   =   midCol+1 <= endCol    &&  mat[maxRow][midCol+1] > mat[maxRow][midCol];
            
            if (rightIsBig) {        // there is an element in 'right' that is bigger than all the elements in the 'midCol' 
                startCol = midCol+1; // so 'midCol' cannot have a 'peakPlane'
            } else if (leftIsBig) {  
                endCol = midCol-1;
            } else { // we have found the peak element
                return new int[]{maxRow, midCol};
            }
        }
        
        return null;
    }
}
```
