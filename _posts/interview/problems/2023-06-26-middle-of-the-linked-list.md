---
layout: post
published: true
title: "876. Middle of the Linked List"
categories: interview
tags: easy linked-list two-pointers
---

> 단일 연결 리스트의 헤드가 주어지면 연결 리스트의 중간 노드를 반환

[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

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
    // Two Pointer
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            head = head.next;
            fast = fast.next.next;
        }
        
        return head;
    }
}
```