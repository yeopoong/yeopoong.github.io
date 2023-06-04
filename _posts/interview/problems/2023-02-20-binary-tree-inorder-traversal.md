---
layout: post
published: true
title: "94. Binary Tree Inorder Traversal"
categories: interview
tags: tree
---

[Easy]

- [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

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
    
    /*
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
    */
}
```
{% gist 46c3c64be0e75dd8b212ff938dee3ac9 %}