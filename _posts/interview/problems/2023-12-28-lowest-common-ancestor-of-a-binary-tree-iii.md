---
layout: post
published: true
title: "1650. Lowest Common Ancestor of a Binary Tree III"
categories: interview
tags: medium tree dfs
---

> 이진 트리 p와 q의 두 노드가 주어지면 해당 노드의 최하위 공통 조상(LCA)을 반환

[1650. Lowest Common Ancestor of a Binary Tree III](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/)

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
};
*/

class Solution {
    public Node lowestCommonAncestor(Node p, Node q) {
        Set<Node> seen = new HashSet<>();
        
        while (p != null) {
            seen.add(p);
            p = p.parent;
        }
        
        while (q != null) {
            if (seen.contains(q)) {
                return q;
            }
            q = q.parent;
        }
        
        return null;
    }
}
```