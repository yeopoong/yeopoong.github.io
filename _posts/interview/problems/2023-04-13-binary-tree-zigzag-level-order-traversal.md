---
layout: post
published: true
title: "103. Binary Tree Zigzag Level Order Traversal"
categories: interview
tags: tree dfs
---

> 이진 트리의 루트가 주어지면 해당 노드 값의 지그재그 수준 순회를 반환

- [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)
![](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/Figures/103/103_DFS.png)

BFS
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
    
    // 이진 트리 지그재그 수준 순서 순회
    // T: O(n)
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        
        if (root == null) return res;
    
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        
        boolean order = false;
        int size = 0;

        while (!queue.isEmpty()) {
            List<Integer> temp = new ArrayList<>();
            order = !order;
            size = queue.size();
            for (int i = 0; i < size; ++i) {
                TreeNode node = queue.poll();
                if (order) {
                    temp.add(node.val);
                } else {
                    temp.add(0, node.val);
                }
                
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
            res.add(temp);
        }
        
        return res;
    }
}
```

DFS
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    
    // 이진 트리 지그재그 수준 순서 순회
    // T: O(n)
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        travel(root, 0);
        
        return result;
    }
    
    // 트리 레벨값에 따라서 리스트의 앞/뒤에 넣는다.
    // T: O(n)
    private void travel(TreeNode curr, int level) {
        if (curr == null) return;
        
        // * 레벨별로 리스트를 생성한다.
        if (result.size() <= level) {
            result.add(new LinkedList<Integer>());
        }
        
        List<Integer> list = result.get(level);
        
        // 왼쪽/오른쪽 순서를 정함
        if (level % 2 == 0) {
            list.add(curr.val); // 왼쪽에서 오른쪽 (15, 7)
        } else {
            list.add(0, curr.val); // 오른쪽에서 왼쪽 (20, 9)
        }
        
        // 왼쪽/오른쪽 순서로 처리해야 한다.
        travel(curr.left, level + 1);
        travel(curr.right, level + 1);
    }
}
```