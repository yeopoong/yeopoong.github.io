---
layout: post
published: true
title: "653. Two Sum IV - Input is a BST"
categories: interview
tags: easy tree dfs
---

> 이진 검색 트리의 루트와 정수 k가 주어지면 BST에 두 개의 요소가 존재하여 합계가 k와 같으면 true를 반환

[653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

![](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_1.jpg)

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
    Set<Integer> seen = new HashSet<>();
    
    // BST에서 Two Sum 
    public boolean findTarget(TreeNode root, int k) {
        return dfs(root, k);
    }
    
    private boolean dfs(TreeNode root, int k) {
        if (root == null) return false;

        // 보수값이 존재하면 투썸이 존재함
        if (seen.contains(k - root.val)) {
            return true;
        } else {
            seen.add(root.val);
        }

        return dfs(root.left, k) || dfs(root.right, k);
    }
}
```