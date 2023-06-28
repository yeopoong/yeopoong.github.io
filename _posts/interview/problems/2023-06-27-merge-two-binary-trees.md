---
layout: post
published: true
title: "617. Merge Two Binary Trees"
categories: interview
tags: easy tree
---

> 두개의 트리가 주어지면 노드값을 병합한 트리를 구하라

[617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/)

![](https://assets.leetcode.com/uploads/2021/02/05/merge.jpg)

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
    //Time complexity : O(m). A total of m nodes need to be traversed. Here, m represents the minimum number of nodes from the two given trees.
    //Space complexity : O(m). The depth of the recursion tree can go upto m in the case of a skewed tree. In average case, depth will be O(log m)
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        // End Condition: 둘 중에 하나가 널이면 널아닌 노드를 사용하면 된다.
        if (root1 == null) return root2;
        if (root2 == null) return root1;
        
        // Merge node: 신규 노드를 생성하고 노드값은 더하고 왼쪽/오른쪽 자식은 재귀로 처리
        TreeNode t = new TreeNode(root1.val + root2.val);
        t.left = mergeTrees(root1.left, root2.left);
        t.right = mergeTrees(root1.right, root2.right);
        
        return t;
    }
}
```