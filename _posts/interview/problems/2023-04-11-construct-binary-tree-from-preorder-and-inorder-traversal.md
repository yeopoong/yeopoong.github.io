---
layout: post
published: true
title: "105. Construct Binary Tree from Preorder and Inorder Traversal"
categories: interview
tags: problems tree recursion
---

> 두 개의 정수 배열 preorder 및 inorder가 주어지면 이진 트리를 구성하고 반환

- [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

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
    private int[] preorder;
    private int[] inorder;

    // 이진트리 구성하기
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        this.inorder = inorder;
        
        return helper(0, 0, inorder.length - 1);
    }

    // 전위순회: root - left - right, 첫번째 인덱스 값이 루트값이다.
    // 중위순회: left - root - right, 좌우 노드를 알 수 있다.
    public TreeNode helper(int preStart, int inStart, int inEnd) {
        if (preStart > preorder.length - 1 || inStart > inEnd) {
            return null;
        }
        
        // 1) 전위순회에서 루트값을 알 수 있다(첫번째 값이 항상 루트 값이다).
        TreeNode root = new TreeNode(preorder[preStart]);
        
        int inIndex = 0; 
        // 2) 중위순회에서 루트의 인덱스를 찾는다. 
        for (int i = inStart; i <= inEnd; i++) {
            if (inorder[i] == root.val) {
                inIndex = i;
                break;
            }
        }
        
        // 3) 중위순회는 오름차순 정렬이기 때문에 오른쪽(작은값), 왼쪽(큰값) 서브트리의 원소들를 알 수 있다.
        // 4) 전위순회에서 다음 루트의 인덱스는 현재 인덱스 + 왼쪽자식의 개수
        root.left = helper(preStart + 1, inStart, inIndex - 1);
        root.right = helper(preStart + inIndex - inStart + 1, inIndex + 1, inEnd);
        
        return root;
    }
}
```