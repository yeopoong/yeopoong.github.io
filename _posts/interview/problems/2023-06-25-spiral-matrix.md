---
layout: post
published: true
title: "54. Spiral Matrix"
categories: interview
tags: medium matrix
---

> 숫자만 포함된 문자열 s가 주어지면 s에 점을 삽입하여 형성할 수 있는 가능한 모든 유효한 IP 주소를 반환

[54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

```java
class Solution {
    
    // 나선 행열
    // T: O(mn)
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        
        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;
        
        while (true) {
            //Top-Right
            for (int i = left; i <= right; i++) res.add(matrix[top][i]);
            top++;
            if (left > right || top > bottom) break;
            
            //Right-Bottom
            for (int i = top; i <= bottom; i++) res.add(matrix[i][right]);
            right--;
            if (left > right || top > bottom) break;
            
            //Bottom-Left
            for (int i = right; i >= left; i--) res.add(matrix[bottom][i]);
            bottom--;
            if (left > right || top > bottom) break;
            
            //Left-Top
            for (int i = bottom; i >= top; i--) res.add(matrix[i][left]);
            left++;
            if (left > right || top > bottom) break;
        }
        
        return res;
    }
}
```
