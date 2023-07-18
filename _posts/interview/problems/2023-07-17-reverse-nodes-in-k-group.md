---
layout: post
published: true
title: "25. Reverse Nodes in k-Group"
categories: interview
tags: hard linked-list
---

> 연결된 목록의 헤드가 주어지면 한 번에 k번 목록의 노드를 뒤집고 수정된 목록을 반환

[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    
    public ListNode reverseKGroup(ListNode head, int k) {
        // 처음에는 헤드를 가리킨다.
        ListNode dummy = new ListNode(0, head);
        
        int n = 0;
        
        // 전체 노드의 개수
        int n = getLength(head);
        
        // 작업노드
        ListNode prev = dummy, node = head, next;
        
        while (n >= k) {
            // 그룹 단위로 리버스 처리한다.
            for (int i = 1; i < k; i++) {
                next = node.next.next;
                node.next.next = prev.next;
                prev.next = node.next;
                node.next = next;
            }
            
            prev = node;
            node = node.next;
            n -= k;
        }
        
        return dummy.next;
    }

    public int getLength(ListNode head) {
        int length = 1;

        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            length += 1;
        }

        return length;
    }
}
```