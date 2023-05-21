---
layout: post
published: true
title: "92. Reverse Linked List II"
categories: interview
tags: problems linked-list
---

> 단일 연결 리스트의 헤드와 왼쪽 <= 오른쪽인 두 개의 정수 왼쪽과 오른쪽이 주어지면 목록의 노드를 왼쪽 위치에서 오른쪽 위치로 반전하고 반전된 목록을 반환

- [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

![](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

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
    
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(0);
        
        dummy.next = head;
        ListNode prev = dummy; 
        
        for (int i = 0; i < left - 1; i++) {
            prev = prev.next; // adjusting the prev pointer on it's actual index
        }
        
        ListNode curr = prev.next; // curr pointer will be just after prev
        
        // reversing
        for (int i = 0; i < right - left; i++) {
            ListNode next = curr.next; // next pointer will be after curr
            curr.next = next.next;
            next.next = prev.next;
            prev.next = next;
        }
        
        return dummy.next;
    } 
}
```