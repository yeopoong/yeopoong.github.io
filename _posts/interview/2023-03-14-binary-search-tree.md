---
layout: post
published: false
title: "Binary Search Tree"
categories: interview
tags: binary-search-tree
---


```java
List<Integer> inorderNodes = new ArrayList<>();
void inorderTraversal(TreeNode node) {
    if (node == null) {
        return;
    }
    
    inorderTraversal(node.left);
    inorderNodes.add(node.val); // Store the nodes in the list.
    inorderTraversal(node.right);
}
```

[Easy]
- [530. Minimum Absolute Difference in BST](/interview/2023/05/29/minimum-absolute-difference-in-bst/)
- [700. Search in a Binary Search Tree](/interview/2023/07/09/search-in-a-binary-search-tree/)

[Medium]
- [96. Unique Binary Search Trees](/interview/2023/05/22/unique-binary-search-trees/)
- [98. Validate Binary Search Tree](/interview/2023/04/16/validate-binary-search-tree/)
- [173. Binary Search Tree Iterator](/interview/2023/05/21/binary-search-tree-iterator/)
- [230. Kth Smallest Element in a BST](/interview/2023/06/05/kth-smallest-element-in-a-bst/)
- [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)