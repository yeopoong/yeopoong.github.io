---
layout: post
published: true
title: "102. Binary Tree Level Order Traversal"
categories: interview
tags: medium tree bfs
---

> 이진 트리의 루트가 주어지면 해당 노드 값의 레벨 순회를 반환 (즉, 왼쪽에서 오른쪽으로, 레벨별로)

[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

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
    // from left to right
    // level by level
    // Output: [[3],[9,20],[15,7]]
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new LinkedList<>();
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        if (root == null) return list;
        
        // 큐에 존재하는 모든 노드를 처리하고 다음 레벨 처리를 위해서 자식노드를 큐에 저장한다.
        while (!queue.isEmpty()) {
            // * size of level
            int level = queue.size();
            
            // level by level
            List<Integer> subList = new LinkedList<>();
            
            // * 현재 큐에 들어 있는 갯수(현재 레벨 노드 갯수) 만큼 꺼내서 처리한다.
            for (int i = 0; i < level; i++) {
                TreeNode node = queue.poll();
                subList.add(node.val);
                
                // 자식노드를 큐에 저장한다(from left to right)
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            list.add(subList);
        }
        
        return list;
    }
}
```