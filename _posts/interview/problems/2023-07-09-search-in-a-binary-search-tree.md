---
layout: post
published: true
title: "700. Search in a Binary Search Tree"
categories: interview
tags: easy binary-search-tree
---

> 이진검색틀의 노드의 값이 val인 노드를 찾고 해당 노드를 기반으로 하는 하위 트리를 반환

[700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)

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
    // 이진 탐색 트리: 왼쪽 < 루트 < 오른쪽
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {
            return null;
        } else if (val < root.val) {
            return searchBST(root.left, val);
        } else if (val > root.val) {
            return searchBST(root.right, val);
        } else {
            return root;
        }
    }
}
```