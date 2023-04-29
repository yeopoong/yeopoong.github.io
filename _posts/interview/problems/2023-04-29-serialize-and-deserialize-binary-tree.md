---
layout: post
published: true
title: "297. Serialize and Deserialize Binary Tree"
categories: interview
tags: problems tree design dfs
---

> 두 개의 이진 문자열 a와 b가 주어지면 합계를 이진 문자열로 반환

- [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    private int index = 0;

    // Encodes a tree to a single string: dfs
    public String serialize(TreeNode root) {
        // 노드의 마지막을 나타낸다. 
        if (root == null) return "#";
        
        // 전위순회(Preorder): 루트 -> 왼쪽 -> 오른쪽
        return root.val + "," + serialize(root.left) + "," + serialize(root.right);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] nodes = data.split(",");
        
        return helper(nodes);
    }
    
    // DFS: O(n)
    private TreeNode helper(String[] nodes) {
        String s = nodes[index++];
        
        // Base case
        if (s.equals("#")) return null;
        
        // Preorder
        TreeNode root = new TreeNode(Integer.parseInt(s));
        root.left = helper(nodes);
        root.right = helper(nodes);
        
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```
