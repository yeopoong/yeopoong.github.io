---
layout: post
published: true
title: "1644. Lowest Common Ancestor of a Binary Tree II"
categories: interview
tags: medium tree dfs
---

> 이진 트리의 루트가 주어지면 주어진 두 노드 p와 q의 최저 공통 조상(LCA)을 반환

[1644. Lowest Common Ancestor of a Binary Tree II](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-ii/)

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

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
    
    // root = [3,5,1,6,2,0,8,null,null,7,4]
    // (5,1), (5,4), (5, 10) represent several diff cases
    int count = 0;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode res = dfs(root, p, q);
        return count == 2 ? res : null;
    }
    
    private TreeNode dfs(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return root;
        
        TreeNode l = dfs(root.left, p, q);
        TreeNode r = dfs(root.right, p, q);
        
        // must calling l and r to get deeper into tree to continue search
        // cannot directly return
        if (root == p || root == q) {
            count++; // need this for (5,10) and (5,4) case
            return root;
        }
        
        if (l != null && r != null) return root;
        
        return (l != null) ? l : r;
    }
}
```