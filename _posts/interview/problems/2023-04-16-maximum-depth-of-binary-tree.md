---
layout: post
published: true
title: "104. Maximum Depth of Binary Tree"
categories: interview
tags: problems tree dfs maximun
---

> 이진 트리의 최대 깊이

- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

```java
class Solution {
    public int maxDepth(TreeNode root) {
        int level = 0;
        
        if (root == null) return 0;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            // 같은 레벨의 노드를 모두 처리한다.
            while (size-- > 0) {
                TreeNode node = queue.poll();
                
                // 다음 레벨 처리를 위해서 왼쪽노드 저장 
                if (node.left != null) {
                    queue.offer(node.left);
                }
                
                // 다음 레벨 처리를 위해서 오른쪽노드 저장 
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            // 깊이가 하나 증가한다.
            level++;
        }
        
        return level;
    }
}
```