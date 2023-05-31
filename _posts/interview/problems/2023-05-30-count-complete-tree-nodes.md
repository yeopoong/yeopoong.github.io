---
layout: post
published: true
title: "222. Count Complete Tree Nodes"
categories: interview
tags: problems tree binary-search
---

> 완전한 이진 트리의 루트가 주어지면 트리의 노드 수를 반환합니다.

- [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)

O(n) time complexity
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
    public int countNodes(TreeNode root) {
         return root != null ? 1 + countNodes(root.right) + countNodes(root.left) : 0;
    }
}
```

O(log(n)^2) time complexity
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
    
    // 완전한 트리 노드 수 계산
    // T: O(n)
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        
        TreeNode left = root, right = root;
        
        int height = 0;
        // 오른쪽 자식이 존재할때까지 높이를 계산한다.
        while (right != null) {
            left = left.left;
            right = right.right;
            height++;
        }
        
        // 만약 왼쪽 자식도 존재하지 않으면  
        if (left == null) return (1 << height) - 1;
        
        return 1 + countNodes(root.left) + countNodes(root.right);
        
        //return root != null ? 1 + countNodes(root.right) + countNodes(root.left) : 0;
    }
}
```