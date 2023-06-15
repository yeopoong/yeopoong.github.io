---
layout: post
published: true
title: "366. Find Leaves of Binary Tree"
categories: interview
tags: tree dfs
---

> 이진 트리의 루트가 주어지면 다음을 수행하는 것처럼 트리의 노드를 수집
> - 모든 리프 노드를 수집  
> - 모든 리프 노드를 제거  
> - 트리가 비워질 때까지 반복  

[366. Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/)

![](https://assets.leetcode.com/uploads/2021/03/16/remleaves-tree.jpg)

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
    
    List<List<Integer>> res = new ArrayList<>();
    
    // 이진 트리의 리프 노드 찾기
    public List<List<Integer>> findLeaves(TreeNode root) {
        dfs(root);
        return res;
    }
    
    // 노드가 수집되는 순서는 노드의 높이(height)에 따라 정해진다.
    // T: O(n)
    private int dfs(TreeNode node){
        // 종료조건
        if (node == null) return -1;
        
        // 재귀호출
        int height = 1 + Math.max(dfs(node.left), dfs(node.right));
        
        if (res.size() == height) {
            res.add(new ArrayList<>());
        }
        
        // 결과처리
        res.get(height).add(node.val);
        
        return height;
    }
}
```