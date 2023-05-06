---
layout: post
published: true
title: "1469. Find All The Lonely Nodes"
categories: interview
tags: problems tree recursion
---

> 이진트리에서 부모 노드의 유일한 자식 노드 찾기

- [1469. Find All The Lonely Nodes](https://leetcode.com/problems/find-all-the-lonely-nodes/)

![](https://assets.leetcode.com/uploads/2020/06/03/e2.png)

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
    
    ArrayList<Integer> nodes = new ArrayList<>();
    
    // 부모 노드의 유일한 자식 노드 찾기
    // T: O(n)
    public List<Integer> getLonelyNodes(TreeNode root) {
        // 루트 노드는 제외한다.
        addLonelyNodes(root, false);
        
        return nodes;
    }
    
    // 왼쪽/오른쪽 노드를 재귀로 순회하면서 자식노드가 하나인 노드를 결과 리스트에 추가 
    private void addLonelyNodes(TreeNode node, boolean lonely) {
        // 종료조건
        if (node == null) return;
        
        // 결과저장
        if (lonely) nodes.add(node.val);

        // 왼쪽노드 처리 
        addLonelyNodes(node.left, node.right == null);
        // 오른쪽노드 처리 
        addLonelyNodes(node.right, node.left == null);
    }
}
```