---
layout: post
published: true
title: "662. Maximum Width of Binary Tree"
categories: interview
tags: problems tree dfs
---

> 이진 트리의 최대 너비 구하기  
> - 트리의 최대 너비(가장 왼쪽 및 가장 오른쪽의 null이 아닌 노드 사이의 길이)

- [662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)

![](https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg)

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

    private int maxWidth = 0;
    
    // map contains the first col_index for each level
    private HashMap<Integer, Integer> map = new HashMap<>();

    // 트리의 최대 너비(가장 왼쪽 및 가장 오른쪽의 null이 아닌 노드 사이의 길이)
    public int widthOfBinaryTree(TreeNode root) {
        dfs(root, 0, 0);

        return this.maxWidth;
    }

    protected void dfs(TreeNode node, int depth, int colIndex) {
        if (node == null) return;
        
        // initialize the value, for the first seen colIndex per level
        if (!map.containsKey(depth)) {
            map.put(depth, colIndex);
        }
        
        int firstColIndex = map.get(depth);

        maxWidth = Math.max(maxWidth, colIndex - firstColIndex + 1);

        // Preorder DFS. Note: it is important to put the priority on the left child
        dfs(node.left, depth + 1, 2 * colIndex);
        dfs(node.right, depth + 1, 2 * colIndex + 1);
    }
}
```