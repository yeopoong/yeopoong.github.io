---
layout: post
published: true
title: "1325. Delete Leaves With a Given Value"
categories: interview
tags: problems tree dfs
---

> 이진 트리 루트와 정수 대상이 주어지면 대상 값이 있는 모든 리프 노드를 삭제

- [1325. Delete Leaves With a Given Value](https://leetcode.com/problems/delete-leaves-with-a-given-value/)

![](https://assets.leetcode.com/uploads/2020/01/09/sample_2_1684.png)

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
    
    // 이진 트리 루트와 정수가 주어지면 대상 값이 있는 모든 리프 노드를 삭제
    // T: O(n)
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        // 종료조건
        if (root == null) return root;
        
        // 재귀호출
        root.left = removeLeafNodes(root.left, target);
        root.right = removeLeafNodes(root.right, target);
        
        // 메인로직: 리프노드이고 값이 target과 동일하면 삭제
        if (root.left == null && root.right == null && root.val == target) {
            return null; 
        } else {
            return root;
        }
    }
}
```