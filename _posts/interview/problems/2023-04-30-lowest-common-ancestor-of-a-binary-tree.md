---
layout: post
published: true
title: "236. Lowest Common Ancestor of a Binary Tree"
categories: interview
tags: problems tree
---

> 이진 트리의 가장 작은 공통 조상 

- [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    
    // 이진 트리의 가장 작은 공통 조상 
    // Find LCA: O(n)
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // 종료조건: 자식이 더 이상 없거나 노드를 찾으면 리턴 
        if (root == null || root == p || root == q) return root;
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        // 왼쪽/오른쪽이 널이면 반대쪽, 아니면 루트가 LCA 이다. 
        return (left == null) ? right : (right == null) ? left : root;
    }
}
```
