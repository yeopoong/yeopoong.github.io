---
layout: post
published: true
title: "572. Subtree of Another Tree"
categories: interview
tags: easy tree dfs
---

> 두 이진 트리 root와 subRoot의 루트가 주어졌을 때 동일한 구조를 가진 root의 하위 트리가 있고 subRoot의 노드 값이 있으면 true를 반환

[572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)

![](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

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
    // 같은 구조의 서브트리 찾기
    // O(m*n)
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) return false;
        
        return isSame(root, subRoot) || isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }
    
    // 두노드가 동일한 구조인지 체크
    private boolean isSame(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        
        // 두노드의 값이 다르면 동일하지 않음
        if (s == null || t == null || s.val != t.val) return false;
        
        // 왼쪽/오른쪽 노드를 재귀로 체크
        return isSame(s.left, t.left) && isSame(s.right, t.right);
    } 
}
```