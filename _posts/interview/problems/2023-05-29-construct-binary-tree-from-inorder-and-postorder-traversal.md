---
layout: post
published: true
title: "106. Construct Binary Tree from Inorder and Postorder Traversal"
categories: interview
tags: problems tree recursion
---

> 두 개의 정수 배열 inorder 및 postorder가 주어지면 이진 트리를 구성하고 반환

- [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

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
    HashMap<Integer, Integer> map = new HashMap<Integer,Integer>();
    private int[] postorder;
    private int[] inorder;
    
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.postorder = postorder;
        this.inorder = inorder;
        
        for (int i = 0; i < inorder.length; ++i) {
            map.put(inorder[i], i);
        }
        
        return buildTreePostIn(0, inorder.length - 1, postorder.length - 1);
    }

    private TreeNode buildTreePostIn(int inStart, int inEnd, int preEnd) {
        if (preEnd >= postorder.length || inStart > inEnd) return null;
        
        // 1) 후위순회에서 루트값을 알 수 있다(마지막 값이 항상 루트 값이다).
        TreeNode root = new TreeNode(postorder[preEnd]);
        
        // 2) 중위순회에서 루트의 인덱스를 찾는다. 
        int rootIndex = map.get(postorder[preEnd]);
        
        root.left = buildTreePostIn(inStart, rootIndex - 1, preEnd - 1 - inEnd + rootIndex);
        root.right = buildTreePostIn(rootIndex + 1, inEnd, preEnd - 1);
        
        return root;
    }
}
```