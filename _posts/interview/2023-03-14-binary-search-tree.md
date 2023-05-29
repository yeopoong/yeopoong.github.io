---
layout: post
published: false
title: "Binary Search Tree"
categories: interview
tags: interview binary-search-tree
---

## Binary Search Tree


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

[Medium]
- [96. Unique Binary Search Trees](/interview/2023/05/21/unique-binary-search-trees/)
- [173. Binary Search Tree Iterator](/interview/2023/05/21/binary-search-tree-iterator/)