---
layout: post
published: true
title: "114. Flatten Binary Tree to Linked List"
categories: interview
tags: medium tree
---

> 이진 트리의 루트가 주어지면 트리를 "연결된 목록"으로 병합

[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

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
    
    public void flatten(TreeNode root) {
        this.flattenTree(root);
    }
    
    private TreeNode flattenTree(TreeNode node) {
        
        if (node == null) {
            return null;
        }
            
        // For a leaf node, we simply return the node as is.
        if (node.left == null && node.right == null) {
            return node;
        }
        
        TreeNode leftTail = flattenTree(node.left);
        TreeNode rightTail = flattenTree(node.right);
        
        // If there was a left subtree, we shuffle the connections around so that there is nothing on the left side anymore.
        if (leftTail != null) {
            leftTail.right = node.right;
            node.right = node.left;
            node.left = null;
        }
        
        // We need to return the "rightmost" node after we are/ done wiring the new connections. 
        return rightTail == null ? leftTail : rightTail;
    }
}
```