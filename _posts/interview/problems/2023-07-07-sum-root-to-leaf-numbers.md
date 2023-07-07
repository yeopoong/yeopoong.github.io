---
layout: post
published: true
title: "129. Sum Root to Leaf Numbers"
categories: interview
tags: medium tree
---

> 0에서 9까지의 숫자만 포함하는 이진 트리에서 루트에서 리프까지의 모든 수의 총합을 반환

[129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

![](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

Recursion
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
    int rootToLeaf = 0;
    
    public int sumNumbers(TreeNode root) {
        preorder(root, 0);
        return rootToLeaf;
    }
    
    public void preorder(TreeNode r, int currNumber) {
        if (r != null) {
            currNumber = currNumber * 10 + r.val;
            // if it's a leaf, update root-to-leaf sum
            if (r.left == null && r.right == null) {
                rootToLeaf += currNumber;
            }
            preorder(r.left, currNumber);
            preorder(r.right, currNumber) ;
        }
    }
}
```