---
layout: post
published: true
title: "652. Find Duplicate Subtrees"
categories: interview
tags: problems tree hashmap
---

> 이진 트리의 루트가 주어지면 모든 중복 하위 트리를 반환  
> 두 트리가 동일한 노드 값을 가진 동일한 구조를 갖는 경우 두 트리가 중복

- [652. Find Duplicate Subtrees](https://leetcode.com/problems/find-duplicate-subtrees/)
![](https://assets.leetcode.com/uploads/2020/08/16/e1.jpg)

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
    
    List<TreeNode> res = new LinkedList<>();
    Map<String, Integer> map = new HashMap<>();
    
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        postorder(root);
        return res;
    }

    public String postorder(TreeNode cur) {
        if (cur == null) {
            return "#";  
        }
        
        String serial = cur.val + "," + postorder(cur.left) + "," + postorder(cur.right);
        map.put(serial, map.getOrDefault(serial, 0) + 1);
        
        if (map.get(serial) == 2) {
            res.add(cur);
        }
        
        return serial;
    }
}
```
