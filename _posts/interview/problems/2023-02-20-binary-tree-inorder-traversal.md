---
layout: post
published: true
title: "94. Binary Tree Inorder Traversal"
categories: interview
tags: easy tree
---

[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

스택을 이용해서 왼쪽자식, 중앙값, 오른쪽 자식순으로 리프노드 나올때까지 쌓으면서 역순으로 처리한다.

iterative inorder traversal
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
    List<Integer> result = new ArrayList<>();
    
    // 이진 트리 중위 순회: left->root->right
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        
        TreeNode node = root;
        
        while (node != null || !stack.isEmpty()) {
            //왼쪽자식이 존재하면 스택에 넣는다. 
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            
            //현재노드(최상위 스택)를 처리한다.
            node = stack.pop();
            result.add(node.val);
            
            //오른쪽자식
            node = node.right;
        }
        
        return result;
    }
}
```

recursive inorder traversal
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        helper(root);
        return result;
    }

    public void helper(TreeNode root) {
        if (root != null) {
            helper(root.left);
            result.add(root.val);
            helper(root.right);
        }
    }
}
```
