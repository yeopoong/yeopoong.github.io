---
layout: post
published: true
title: "138. Copy List with Random Pointer"
categories: interview
tags: linked-list hashmap
---

> 목록의 전체 복사본을 구성: 새 목록의 어떤 포인터도 원래 목록의 노드를 가리켜서는 안됨

[138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    
    // 목록의 전체 복사본을 구성: 새 목록의 어떤 포인터도 원래 목록의 노드를 가리켜서는 안됨
    // T: O(n)
    public Node copyRandomList(Node head) {
        
        // { key=old node, value=new node }
        Map<Node, Node> map = new HashMap<>();

        // 1. 기존노드를 키로 신규노드를 생성해서 저장한다.
        Node node = head;
        while (node != null) {
            map.put(node, new Node(node.val));
            node = node.next;
        }

        // 2. assign next and random pointers
        node = head;
        while (node != null) {
            map.get(node).next = map.get(node.next);
            map.get(node).random = map.get(node.random);
            node = node.next;
        }

        // 신규노드의 헤더를 리턴
        return map.get(head);
    }
}
```