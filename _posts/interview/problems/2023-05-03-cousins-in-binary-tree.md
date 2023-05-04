---
layout: post
published: true
title: "993. Cousins in Binary Tree"
categories: interview
tags: problems tree hashmap
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
