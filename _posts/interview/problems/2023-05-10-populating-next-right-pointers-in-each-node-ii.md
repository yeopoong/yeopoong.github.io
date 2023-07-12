---
layout: post
published: true
title: "117. Populating Next Right Pointers in Each Node II"
categories: interview
tags: medium tree bfs
---

> 각 노드에서 다음 오른쪽 포인터 채우기

[117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    // 각 노드의 다음 오른쪽 포인터 채우기
    public Node connect(Node root) {
        if (root == null) return null;
        
        // 오른쪽 노드부터 입력한 순서대로 처리하기 위해서 큐를 사용
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        
        while (!q.isEmpty()) {
            // 같은 레벨의 노드를 처리하기 위해서 큐의 데이터 개수 단위로 반복
            int size = q.size();
            
            // 가장 오른쪽 노드는 널이다.
            Node nextPointer = null;
            
            for (int i = 0; i < size; i++) {
                Node node = q.poll();
                node.next = nextPointer;
                nextPointer = node;
                
                // 오른쪽 노드부터 처리
                if (node.right != null) q.add(node.right);
                if (node.left != null) q.add(node.left);
            }
        }
        
        return root;
    }
}
```
