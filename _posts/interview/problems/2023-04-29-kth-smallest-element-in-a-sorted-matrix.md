---
layout: post
published: true
title: "378. Kth Smallest Element in a Sorted Matrix"
categories: interview
tags: problems array matrix heap binary-search
---

> 각 행과 열이 오름차순으로 정렬된 n x n 행렬이 주어지면 행렬에서 k번째로 작은 요소를 반환

- [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

```java
class Solution {
    // 행렬에서 k번째로 작은 요소를 반환
    public int kthSmallest(int[][] matrix, int k) {
        int ans = -1; 
        
        // For general, the matrix need not be a square
        int m = matrix.length, n = matrix[0].length; 
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>(Comparator.comparingInt(o -> o[0]));
        
        for (int r = 0; r < Math.min(m, k); ++r) {
            minHeap.offer(new int[]{matrix[r][0], r, 0});
        }

        for (int i = 1; i <= k; ++i) {
            int[] top = minHeap.poll();
            int r = top[1], c = top[2];
            ans = top[0];
            if (c + 1 < n) minHeap.offer(new int[]{matrix[r][c + 1], r, c + 1});
        }
        
        return ans;
    }
}
```
