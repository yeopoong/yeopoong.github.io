---
layout: post
published: true
title: "230. Kth Smallest Element in a BST"
categories: interview
tags: medium binary-search-tree
---

> 이진 검색 트리의 루트와 정수 k가 주어지면 트리의 모든 노드 값 중 k번째로 작은 값을 반환

[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

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
    List<Integer> result = new ArrayList<>();
    
    // K번째 가장 작은 요소(중위순회로 리스트에 저장하고 K번째 요소를 리턴)
    public int kthSmallest(TreeNode root, int k) {
        inorder(root);
        
        return result.get(k - 1);
    }
    
    //inorder traversal of BST is an array sorted in the ascending order.
    public void inorder(TreeNode root) {
        if (root == null) return;
        
        inorder(root.left);
        result.add(root.val);
        inorder(root.right);
    }
}
```

```java    
class Solution {
    List<Integer> result = new ArrayList<>();
    
    // K번째 가장 작은 요소(중위순회로 리스트에 저장하고 K번째 요소를 리턴)
    public int kthSmallest(TreeNode root, int k) {
        return inorder(root, k);
    }
    
    public int inorder(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();

        // 중위순회 하면서 K번째 값을 리턴한다.
        while(root != null || !stack.isEmpty()) {
            // 가장 작은값이 스택의 최상위가 된다.
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            
            // K번째 노드이면  
            if (--k == 0) break;
            
            // 오른쪽 노드를 처리한다.
            root = root.right;
        }
        
        return root.val;
    }
}
```
