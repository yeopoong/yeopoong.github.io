---
layout: post
published: true
title: "124. Binary Tree Maximum Path Sum"
categories: interview
tags: problems dfs tree
---

> 이진 트리의 최대 경로 합계 구하기: DFS

- [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

The path sum of a path is the sum of the node's values in the path.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int maxSum = Integer.MIN_VALUE;
    
    // 이진 트리 최대 경로 합계
    // DFS
    // T: O(n)
    public int maxPathSum(TreeNode root) {
        dfs(root);
        return maxSum;
    }

    // 현재 노드의 자식 노드를 재귀로 순회하면서 합을 구한다.
    public int dfs(TreeNode root) {
        // 종료조건
        if (root == null) return 0;

        // 재귀호출
        // 왼쪽 또는 오른쪽이 0 보다 작으면 합계에 포함시키지 않기 위해서 0으로 만든다. 
        int left = Math.max(0, dfs(root.left));
        int right = Math.max(0, dfs(root.right));
        
        // 현재까지 최대합을 갱신한다.
        this.maxSum = Math.max(maxSum, root.val + left + right);

        // 리턴값은 현재노드 + 왼쪽/오른쪽 노드합의 최대값이다.
        return root.val + Math.max(left, right);
    }
}
```