---
layout: post
published: true
title: "993. Cousins in Binary Tree"
categories: interview
tags: tree hashmap
---

> 고유한 값을 가진 이진 트리의 루트와 트리 x 및 y의 서로 다른 두 노드 값이 주어지면, 트리의 값 x 및 y에 해당하는 노드가 사촌이면 true를 반환하고 그렇지 않으면 false를 반환  
> 이진 트리의 두 노드는 다른 부모와 동일한 깊이를 갖는 경우 사촌

- [993. Cousins in Binary Tree](https://leetcode.com/problems/cousins-in-binary-tree/)
![](https://assets.leetcode.com/uploads/2019/02/12/q1248-01.png)

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
    
    TreeNode xParent = null, yParent = null;
    int xDepth = -1, yDepth = -2;
    
    // T: O(n)
    public boolean isCousins(TreeNode root, int x, int y) {
        dfs(root, null, x, y, 0);
        return xDepth == yDepth && xParent != yParent;
    }
    
    void dfs(TreeNode root, TreeNode parent, int x, int y, int depth) {
        if (root == null) return;
        
        if (x == root.val) {
            xParent = parent;
            xDepth = depth;
        } else if (y == root.val) {
            yParent = parent;
            yDepth = depth;
        } else {
            // if we found x node or found y node then we don't need to dfs deeper
            // because x and y must be the same depth
            dfs(root.left, root, x, y, depth + 1);
            dfs(root.right, root, x, y, depth + 1);
        }
    }
}
```
