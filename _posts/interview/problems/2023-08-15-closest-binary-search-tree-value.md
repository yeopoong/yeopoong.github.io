---
layout: post
published: true
title: "270. Closest Binary Search Tree Value"
categories: interview
tags: easy binary-search-tree
---

> 이진 검색 트리의 루트와 대상 값이 주어지면 대상에 가장 가까운 BST의 값을 반환

[270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/)

![](https://assets.leetcode.com/uploads/2021/03/12/closest1-1-tree.jpg)

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
    public int closestValue(TreeNode root, double target) {
        int result = root.val;   
        
        while (root != null) {
            // 차이값이 더 작으면 결과값을 바꾼다.
            if (Math.abs(target - root.val) < Math.abs(target - result)) {
                result = root.val;
                if (Math.abs(target - root.val) <= 0.5)
					break;
            }      
            root = (root.val > target) ? root.left : root.right;
        }     
        
        return result;
    }
}
```