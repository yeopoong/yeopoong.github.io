---
layout: post
published: true
title: "226. Invert Binary Tree"
categories: interview
tags: easy tree
---

> 이진 트리의 루트가 주어지면 트리를 반전하고 루트를 반환

[226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

![](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

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
    public TreeNode invertTree(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        TreeNode node; 
        TreeNode temp;
        
        //preorder traversal
        while (!stack.isEmpty()) {
            node = stack.pop();
            if (node != null) {
                //invert the tree (서브트리도 변경된다)
                temp = node.left;
                node.left = node.right;
                node.right = temp;
                
                //자식노드처리
                stack.push(node.right);
                stack.push(node.left);
            }
        }
        
        return root;
    }
}
```