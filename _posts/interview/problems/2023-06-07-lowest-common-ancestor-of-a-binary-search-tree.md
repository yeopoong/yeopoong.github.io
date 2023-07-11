---
layout: post
published: true
title: "235. Lowest Common Ancestor of a Binary Search Tree"
categories: interview
tags: medium tree
---

> 이진 검색 트리(BST)에서 주어진 두 노드 중 가장 낮은 공통 조상(LCA) 노드를 검색  
> - 가장 낮은 공통 조상은 두 노드 p와 q 사이에서 p와 q를 모두 자손으로 갖는 T의 가장 낮은 노드로 정의(여기서 노드는 자신의 자손이 될 수 있다)."

[235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

Iterative Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    // 이진 탐색 트리의 최하위(값이 가장 작은) 공통 조상: 중간값인 조상노드를 찾는 문제이다.
    // O(lon n), O(1)
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        int small = Math.min(p.val, q.val);
        int large = Math.max(p.val, q.val);
        
        // 현재노드(root)의 왼쪽/오른쪽 노드로 이동하면서 값을 비교
        while (root != null) {
            if (root.val > large) { // 큰값보다 크면 왼쪽 서브트리에 있다 
                root = root.left;
            } else if (root.val < small) { // 작은값보다 작으면 오른쪽 서브트리에 있다.
                root = root.right;
            } else { // Now, small <= root.val <= large -> This is the LCA between p and q
                return root;
            }
        }
               
        return null;
    }
}
```

Recursive Solution
```java
class Solution {
    // 이진 탐색 트리의 최하위(값이 가장 작은) 공통 조상: 중간값인 조상노드를 찾는 문제이다.
    // O(lon n), O(1)
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        
        if (p.val > root.val && q.val > root.val) {
            return lowestCommonAncestor(root.right, p, q);
        }
        
        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        }
        
        return root;
    }
}
```
