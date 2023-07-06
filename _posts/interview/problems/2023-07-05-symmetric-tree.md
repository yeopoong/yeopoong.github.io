---
layout: post
published: true
title: "101. Symmetric Tree"
categories: interview
tags: easy tree
---

> 이진 트리의 루트가 주어지면 그것이 자신의 거울(즉, 중심을 중심으로 대칭)인지 확인

[101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

**재귀호출**을 이용해서 루트의 좌/우 노드가 같은지를 체크한다.

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
    // 대칭 트리: symmetric around its center
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root.left, root.right);
    }
    
    // 대칭조건: 자식노드와 좌우 노드값이 동일하면 대칭이다.
    private boolean isMirror(TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;
        if (left == null || right == null || left.val != right.val) return false;

        // 왼쪽, 오른쪽 자식노드를 대칭으로 비교한다.
        return isMirror(left.left, right.right) && isMirror(left.right, right.left);
    }
}
```

Iterative
```java
class Solution {
    
    // 대칭 트리: symmetric around its center
    // T: O(n)
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root.left);
        q.add(root.right);
        
        while (!q.isEmpty()) {
            TreeNode t1 = q.poll();
            TreeNode t2 = q.poll();
            if (t1 == null && t2 == null) continue;
            if (t1 == null || t2 == null || t1.val != t2.val) return false;
            q.add(t1.left);
            q.add(t2.right);
            q.add(t1.right);
            q.add(t2.left);
        }
        
        return true;
    }
}
```