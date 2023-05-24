---
layout: post
published: true
title: "863. All Nodes Distance K in Binary Tree"
categories: interview
tags: problems monotonic-stack design
---

> 이진 트리의 노드에서 거리가 k인 모든 노드의 값 배열을 반환

- [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/28/sketch0.png)

```java
class Solution {
        
    Map<TreeNode, Integer> map = new HashMap<>();
    List<Integer> res = new LinkedList<>();
        
    // target 노드에서 k 거리에 있는 모든 노드의 값 배열
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        find(root, target);
        dfs(root, target, K, map.get(root));
        return res;
    }
    
    // find target node first and store the distance in that path that we could use it later directly
    private int find(TreeNode root, TreeNode target) {
        if (root == null) return -1;
        
        if (root == target) {
            map.put(root, 0);
            return 0;
        }
        
        int left = find(root.left, target);
        if (left >= 0) {
            map.put(root, left + 1);
            return left + 1;
        }
        
		int right = find(root.right, target);
		if (right >= 0) {
            map.put(root, right + 1);
            return right + 1;
        }
        
        return -1;
    }
    
    private void dfs(TreeNode root, TreeNode target, int K, int length) {
        if (root == null) return;
        
        if (map.containsKey(root)) {
            length = map.get(root);
        }
        
        if (length == K) {
            res.add(root.val);
        }
        
        dfs(root.left, target, K, length + 1);
        dfs(root.right, target, K, length + 1);
    }
}

```