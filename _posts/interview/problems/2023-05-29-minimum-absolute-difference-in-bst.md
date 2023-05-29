---
layout: post
published: true
title: "530. Minimum Absolute Difference in BST"
categories: interview
tags: problems binary-search-tree
---

> 이진 검색 트리(BST)의 루트가 주어지면 트리에 있는 두 개의 다른 노드 값 사이의 최소 절대 차이를 반환

- [530. Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)

![](https://assets.leetcode.com/uploads/2021/02/05/bst1.jpg)

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
    
    // List to store the tree nodes in the inorder traversal.
    List<Integer> inorderNodes = new ArrayList<>();
    
    // BST의 최소 절대 차이
    // BST를 중위순회하면 정렬된 순으로 리스트를 얻을 수 있다.
    // T: O(n)
    public int getMinimumDifference(TreeNode root) {
        inorderTraversal(root);
        
        int min = Integer.MAX_VALUE;
        
        // Find the diff between every two consecutive values in the list.
        for (int i = 1; i < inorderNodes.size(); i++) {
            min = Math.min(min, inorderNodes.get(i) - inorderNodes.get(i-1));
        }
        
        return min;
    }
    
    void inorderTraversal(TreeNode node) {
        if (node == null) {
            return;
        }
        
        inorderTraversal(node.left);
        inorderNodes.add(node.val); // Store the nodes in the list.
        inorderTraversal(node.right);
    }
}
```