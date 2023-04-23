---
layout: post
published: true
title: "430. Flatten a Multilevel Doubly Linked List"
categories: interview
tags: problems linked-list
---

> 다단계 이중 연결 리스트를 평면화하고 병합된 리스트의 헤드를 반환

- [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
};
*/

class Solution {
    
    // 다단계 이중 연결 목록 평면화
    // DFS by Recursion
    // T: O(n)
    public Node flatten(Node head) {
        Node p = head; 
        
        while (p != null) {
            // 자식노드가 존재하면 처리한다.
            if (p.child != null) {
                // 현재노드의 다음노드 저장
                Node right = p.next; 
                
                // 자식노드 평면화 
                p.next = flatten(p.child);
                
                // 이전노드 설정
                p.next.prev = p;
                
                // 자식 포인터 null로 설정
                p.child = null; 
                         
                // 자식노드의 마지막으로 이동
                while (p.next != null) {
                    p = p.next;
                }
                
                if (right != null) { 
                    // 자식노드의 마지막노드에서 현재노드의 오른쪽 노드를 연결
                    p.next = right;
                    // 이전노드 설정
                    right.prev = p; 
                }
            }
            // 다음노드로 이동
            p = p.next;
        }
        
        return head; 
    }
}
```