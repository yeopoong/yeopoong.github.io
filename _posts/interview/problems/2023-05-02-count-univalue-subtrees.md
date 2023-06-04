---
layout: post
published: true
title: "250. Count Univalue Subtrees"
categories: interview
tags: tree dfs
---

> 이진 트리의 루트가 주어지면 단일 값 하위 트리의 수를 반환

- [250. Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees/)

![](https://assets.leetcode.com/uploads/2020/08/21/unival_e1.jpg)

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
    
    int count;
    
    // 이진 트리의 루트가 주어지면 단일 값 하위 트리의 수를 반환
    public int countUnivalSubtrees(TreeNode root) {
        helper(root);
        
        return this.count;
    }
    
    private boolean helper(TreeNode node) {
        if (node == null) {
            return true;
        }
        
        boolean left = helper(node.left);
        boolean right = helper(node.right);
        
        // 자식노드가 단일값 이면
        if (left && right) {
            // 왼쪽 노드 체크
            if (node.left != null && node.val != node.left.val) {
                return false;
            }
            
            // 오른쪽 노드 체크
            if (node.right != null && node.val != node.right.val) {
                return false;
            }
            
            this.count++;
            
            return true;
        }
        
        return false;
    }
}
```
