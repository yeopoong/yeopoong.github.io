---
layout: post
published: true
title: "543. Diameter of Binary Tree"
categories: interview
tags: problems tree dfs
---

> 이진 트리의 루트가 주어지면 트리 지름(두 노드간의 가장 긴 경로)의 길이를 반환합니다.

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

- [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

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
    int diameter = 0;

    // 이진트리의 두 노드간의 가장 긴 경로
    public int diameterOfBinaryTree(TreeNode root) {
        longestPath(root);
        return diameter;
    }

    private int longestPath(TreeNode node) {
        if (node == null) return 0;
        
        int leftDepth = longestPath(node.left);
        int rightDepth = longestPath(node.right);
        
        // 왼쪽에서 오른쪽까지 가장 긴 값
        diameter = Math.max(diameter, leftDepth + rightDepth);
        
        return 1 + Math.max(leftDepth, rightDepth);
    }
}
```