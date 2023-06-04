---
layout: post
published: true
title: "96. Unique Binary Search Trees"
categories: interview
tags: tree binary-search-tree dynamic-programming
---

> 정수 n이 주어지면 1에서 n까지 고유한 값의 정확히 n개의 노드를 갖는 구조적으로 고유한 BST(이진 검색 트리)의 수를 반환

- [96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

```java
class Solution {
    // 구조적으로 고유한 BST(이진 검색 트리)의 수
    // T: O(n^2), S: O(n)
    public int numTrees(int n) {
        // numTree[4] = numTree[0] * numTree[3] + 
        //              numTree[1] * numTree[2] + 
        //              numTree[2] * numTree[1] + 
        //              numTree[3] * numTree[1]
        
        int [] dp = new int[n+1];
        
        dp[0] = 1; // o nodes = 1 tree (곱을 위해서 1로 지정해야 함)
        dp[1] = 1; // 1 nodes = 1 tree
        
        for (int nodes = 2; nodes <= n; nodes++) {
            int total = 0;
            
            for (int root = 1; root <= nodes; root++) {
                // 왼쪽 트리의 수 * 오른쪽 트리의 수
                int left = root - 1;
                int right = nodes - root;
                total += dp[left] * dp[right];
            }
            
            dp[nodes] = total; 
        }
        
        return dp[n];
    }
}
```