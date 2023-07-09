---
layout: post
published: true
title: "145. Binary Tree Postorder Traversal"
categories: interview
tags: easy tree
---

> 이진 트리의 루트가 주어지면 해당 노드 값의 후위 순회를 반환

[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

![](https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg)

스택을 이용해서 중앙값, 왼쪽자식, 오른쪽 자식순으로 리프노드 나올때까지 쌓으면서 역순으로 처리한다.

iterative postorder traversal
```java
class Solution {
    LinkedList<Integer> result = new LinkedList<>();
    
    // 이진 트리 후위 순회: left->right->root
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        
        if (root == null) return result;

        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.addFirst(node.val);
            
            if (node.left != null) {
                stack.push(node.left);
            }
            
            if (node.right != null) {
                stack.push(node.right);
            } 
        }
        
        return result;
    }
}
```

recursive postorder traversal
```java
class Solution {
    LinkedList<Integer> result = new LinkedList<>();
    
    public List<Integer> postorderTraversal(TreeNode root) {
        traversal(root);
        
        return result;
    }
    
    private void traversal(TreeNode root) {
        if (root != null) {
            traversal(root.left);
            traversal(root.right);
            result.add(root.val);
        }
    }
}
```
