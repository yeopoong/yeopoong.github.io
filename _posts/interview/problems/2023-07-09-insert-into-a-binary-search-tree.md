---
layout: post
published: true
title: "701. Insert into a Binary Search Tree"
categories: interview
tags: medium binary-search-tree
---

> 이진검색트에 신규노드를 삽입 후 루트 노드를 반환

[701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

![](https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg)

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
    // 이진 검색 트리에 삽입(새 값이 원래 BST에 존재하지 않는다)
    // 가장 쉬운 방법은 리프노에 추가하는 것이다.
    public TreeNode insertIntoBST(TreeNode root, int val) {
        // 종료조건: 노드가 존재하지 않으면 새로 생성한다.
        if (root == null) {
            return new TreeNode(val);
        }
        
        // 크면 오른쪽으로 보낸다.
        if (root.val < val) {
            root.right = insertIntoBST(root.right, val);
        // 작으면 왼쪽으로 보낸다.
        }  else {
            root.left = insertIntoBST(root.left, val);
        }
            
        return root;
    }
}
```