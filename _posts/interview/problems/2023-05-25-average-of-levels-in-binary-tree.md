---
layout: post
published: true
title: "637. Average of Levels in Binary Tree"
categories: interview
tags: problems tree bfs
---

> 이진 트리의 루트가 주어지면 각 수준의 노드 평균값을 배열 형태로 반환

- [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/)

![](https://assets.leetcode.com/uploads/2021/03/09/avg1-tree.jpg)

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
    
    // 이진 트리의 수준 평균
    // T: O(n)
    public List<Double> averageOfLevels(TreeNode root) {
        List <Double> res = new ArrayList<>();
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        
        while (!queue.isEmpty()) {
            long sum = 0, count = 0;
            
            Queue<TreeNode> temp = new LinkedList<>();
            while (!queue.isEmpty()) {
                TreeNode n = queue.remove();
                sum += n.val;
                count++;
                if (n.left != null) temp.add(n.left);
                if (n.right != null) temp.add(n.right);
            }
            queue = temp;
            
            res.add(sum * 1.0 / count);
        }
        
        return res;
    }
}
```