---
layout: post
published: true
title: "10. Regular Expression Matching"
categories: interview
tags: problems tree binary-search-tree recursion
---

> 입력 문자열 s와 패턴 p가 주어지면 '.'을 지원하는 정규식 일치를 구현  
> '.' Matches any single character.​​​​  
> '*' Matches zero or more of the preceding element.  

- [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

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