---
layout: post
published: true
title: "199. Binary Tree Right Side View"
categories: interview
tags: problems tree dfs
---

> 이진 트리의 루트가 주어지면 오른쪽에 서 있는 자신을 상상하고 위에서 아래로 정렬된 노드의 값을 반환

![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

- [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

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
    
    // 이진 트리 오른쪽 뷰 
    // O(n): 모든 노드를 방문해야 하므로 
    public List<Integer> rightSideView(TreeNode root) {
        rightView(root, 0);
        
        return result;
    }
    
    // 가장 오른쪽 노드에서 시작해서 왼쪽으로 체크한다.(최초의 오른쪽 노드 찾기)
    public void rightView(TreeNode node, int depth){
        if (node == null) {
            return;
        }
        
        // * 아직 값이 리스트에 들어가 있지 않으면(현재뎁스와 결과 리스트 사이즈가 동일하면) 최초로 보이는 값이므로 이값을 추가한다.
        if (depth == result.size()) {
            result.add(node.val);
        }
        
        rightView(node.right, depth + 1);
        rightView(node.left, depth + 1);
    }
}
```