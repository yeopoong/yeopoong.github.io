---
layout: post
published: true
title: "111. Minimum Depth of Binary Tree"
categories: interview
tags: tree dfs
---

> 이진 트리가 주어지면 최소 깊이를 찾으십시오.  
> - 최소 깊이는 루트 노드에서 가장 가까운 리프 노드까지의 최단 경로에 있는 노드의 수

[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

![](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

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
    
    // 이진 트리의 최소 깊이
    // T: O(n)
    public int minDepth(TreeNode root) {
        return dfs(root);
    }
    
    private int dfs(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        // If only one of child is non-null, then go into that recursion.
        if (root.left == null) {
            return 1 + dfs(root.right);
        } else if (root.right == null) {
            return 1 + dfs(root.left);
        } else {
            // Both children are non-null, hence call for both childs.
            return 1 + Math.min(dfs(root.left), dfs(root.right));
        }
    }
}
```