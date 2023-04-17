---
layout: post
published: true
title: "173. Binary Search Tree Iterator"
categories: interview
tags: problems tree binary-search-tree design
---

> BST(이진 검색 트리)의 순회에 대한 반복자를 나타내는 BSTIterator 클래스를 구현

- [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

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
class BSTIterator {
    private Stack<TreeNode> stack = new Stack<>();
    
    // in-order traversal: 왼쪽/루트/오른쪽
    public BSTIterator(TreeNode root) {
        pushAll(root);
    }

    // Returns true if there exists a number in the traversal to the right of the pointer, otherwise returns false.
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    // Moves the pointer to the right, then returns the number at the pointer.
    public int next() {
        TreeNode node = stack.pop();
        // 오른쪽 노드를 처리한다.
        pushAll(node.right);
        
        return node.val;
    }
    
    // 왼쪽 노드를 스택에 넣는다.
    private void pushAll(TreeNode node) {
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```