---
layout: post
published: true
title: "206. Reverse Linked List"
categories: interview
tags: linked-list easy
---

> 단일 연결 목록의 헤드가 주어지면 목록을 뒤집고 반전된 목록을 반환

[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

연결 리스트의 이전노드, 현재노드, 다음노드의 포인터를 반전시키면서 마지막 노드까지 처리한다.

Recursive
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode p = reverseList(head.next);
        head.next.next = head;
        head.next = null;

        return p;
    }
}
```

Iterative
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
    // 현재노드, 이전노드, 다음노드를 이동하면서 마지막 노드까지 진행한다.
    public ListNode reverseList(ListNode head) {
        ListNode node = head;
        ListNode prev = null;
        ListNode next = null;
        
        while (node != null) {
            // 다음노드를 저장하고
            next = node.next;
            // 현재노드의 포인터를 이전노드로 만들고
            node.next = prev;
            // 이전노드는 현재노드로
            prev = node;
            // 현재노드는 다음노드로 진행한다.
            node = next;
        }
        
        // 마지막 노드(이전노드)가 헤드가 된다.
        return prev;
    }
}
```
