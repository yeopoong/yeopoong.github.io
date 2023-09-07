---
layout: post
published: true
title: "1198. Find Smallest Common Element in All Rows"
categories: interview
tags: medium array
---

> 모든 행이 엄격하게 증가하는 순서로 정렬되는 m x n 행렬 매트가 주어지면 모든 행에서 가장 작은 공통 요소를 반환

[1198. Find Smallest Common Element in All Rows](https://leetcode.com/problems/find-smallest-common-element-in-all-rows/)

```java
class Solution {
    public int smallestCommonElement(int[][] mat) {
        int[] count = new int[10001];
        
        int n = mat.length, m = mat[0].length;
        for (int j = 0; j < m; ++j)
            for (int i = 0; i < n; ++i)
                if (++count[mat[i][j]] == n)
                    return mat[i][j];
        
        return -1;
    }
}
```