---
layout: post
published: true
title: "144. Binary Tree Preorder Traversal"
categories: interview
tags: easy tree
---

> 이진 트리의 루트가 주어지면 해당 노드 값의 사전 순회를 반환

[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

스택을 이용해서 중앙값, 왼쪽자식, 오른쪽 자식순으로 리프노드 나올때까지 쌓으면서 역순으로 처리한다.

iterative preorder traversal
```java
class Solution {
    
    List<Integer> result = new ArrayList<>();
    
    // 전위순회
    public List<Integer> preorderTraversal(TreeNode root) {
        helper(root);
    }
    
    private void helper(TreeNode root) {
        if (root != null) {
            result.add(root.val);
            helper(root.left);
            helper(root.right);
        }
    }
}
```

recursive preorder traversal
```java
class Solution {
    
    List<Integer> result = new ArrayList<>();
    
    // 전위순회
    public List<Integer> preorderTraversal(TreeNode root) {
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node != null) {
                // 루트 노드를 먼저 처리한다.
                result.add(node.val);
                // 스택을 사용하므로 나중값(오른쪽)을 먼저 넣어야 한다.
                stack.push(node.right);
                stack.push(node.left);
            }
        }
        
        return result;
    }
}
```
