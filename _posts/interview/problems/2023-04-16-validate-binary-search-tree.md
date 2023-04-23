---
layout: post
published: true
title: "98. Validate Binary Search Tree"
categories: interview
tags: problems tree binary-search-tree recursion
---

> 이진 트리의 루트가 주어지면 유효한 이진 검색 트리(BST)인지 확인

- [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

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
    
    // Binary Search Tree (BST)
    // 이진 검색 트리 유효성 검사
    public boolean isValidBST(TreeNode root) {
        return checkBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    private boolean checkBST(TreeNode node, long left, long right) {
        if (node == null) return true;
        
        // 루트노드는 왼쪽보다 크고 오른쪽보다 작아야 한다.
        if (!(left < node.val && node.val < right)) return false;

        // Both the left and right subtrees must also be binary search trees.
        return checkBST(node.left, left, node.val) && checkBST(node.right, node.val, right);
    }
}
```