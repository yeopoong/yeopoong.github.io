---
layout: post
published: true
title: "116. Populating Next Right Pointers in Each Node"
categories: interview
tags: problems tree bfs
---

> 각 노드에서 다음 오른쪽 포인터 채우기

- [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

![](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

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
    // 각 노드에서 다음 오른쪽 포인터 채우기
    // O(n)
    public Node connect(Node root) {
        Node node = root;
        
        while (node != null) {
            // 레벨별로 처리하기 위한 변수
            Node cur = node;
            
            // 현재 노드를 기준으로 자식 노드들를 처리한다.
            while (cur != null) {
                // 왼쪽 노드 처리
                if (cur.left != null) {
                    // 왼쪽노드의 다음노드는 오른쪽 노드이다.
                    cur.left.next = cur.right;
                }
                // 오른쪽 노드 처리
                if (cur.right != null && cur.next != null) {
                    // 오른쪽노드의 다음노드는 다음 노드의 오른쪽 노드이다.
                    cur.right.next = cur.next.left;
                }
                
                // 다음 노드로 넘어간다.
                cur = cur.next;
            }
            
            // 다음 왼쪽 레벨로 내력가서 처리한다.
            node = node.left;
        }
        
        return root;
    }
}
```
